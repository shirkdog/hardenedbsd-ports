# Created by: Johannes Dieterich <jmd@FreeBSD.org>
# $FreeBSD$

PORTNAME=	drm-current-kmod
PORTVERSION=	4.16.g20191120
CATEGORIES=	graphics kld

MAINTAINER=	x11@FreeBSD.org
COMMENT=	DRM modules for the linuxkpi-based KMS components

LICENSE=	BSD2CLAUSE MIT GPLv2
LICENSE_COMB=	multi

ONLY_FOR_ARCHS=	amd64 i386 powerpc64
ONLY_FOR_ARCHS_REASON=	the new KMS components are only supported on amd64 and i386

RUN_DEPENDS=	gpu-firmware-kmod>=g20180319:graphics/gpu-firmware-kmod

CONFLICTS_INSTALL=	drm-devel-kmod \
			drm-fbsd11.2-kmod \
			drm-fbsd12.0-kmod \
			drm-legacy-kmod

OPTIONS_DEFINE=	DEBUG SOURCE

OPTIONS_DEFAULT=	SOURCE

SOURCE_DESC=	Install kernel module sources

OPTIONS_SUB=	yes

USES=		kmod uidfix compiler:c++11-lang

USE_GITHUB=	yes
GH_ACCOUNT=	FreeBSDDesktop
GH_PROJECT=	kms-drm
GH_TAGNAME=	f9869ff

.include <bsd.port.options.mk>

.if ${OPSYS} == FreeBSD && ${OSVERSION} < 1300029
IGNORE=		not supported on older CURRENT, no kernel support
.endif
.if ${OPSYS} != FreeBSD
IGNORE=		not supported on anything but FreeBSD (missing linuxkpi functionality)
.endif

.if ${ARCH} == "amd64"
PLIST_SUB+=	AMDGPU=""
PLIST_SUB+=	AMDKFD=""
PLIST_SUB+=	I915=""
PLIST_SUB+=	VMWGFX=""
.elif ${ARCH} == "i386"
PLIST_SUB+=	AMDGPU="@comment "
PLIST_SUB+=	AMDKFD="@comment "
PLIST_SUB+=	I915=""
PLIST_SUB+=     VMWGFX=""
.elif ${ARCH} == "powerpc64"
PLIST_SUB+=	AMDGPU=""
PLIST_SUB+=	AMDKFD="@comment " 
PLIST_SUB+=	I915="@comment "
PLIST_SUB+=     VMWGFX="@comment "
.else
PLIST_SUB+=	AMDGPU="@comment "
PLIST_SUB+=	AMDKFD="@comment "
PLIST_SUB+=	I915="@comment "
PLIST_SUB+=     VMWGFX="@comment "
.endif

KMODSRC=	${STAGEDIR}${PREFIX}/sys/modules/${PORTNAME}
SRCDIRS=	amd drivers drm i915 include linuxkpi radeon ttm vmwgfx

PLIST_SUB+=	KMODSRC="sys/modules/${PORTNAME}"

MAKE_ENV+=	MAKEOBJDIRPREFIX=${WRKSRC}/obj

pre-build:
		${MKDIR} ${WRKSRC}/obj
		(cd ${WRKSRC} ; ${SETENV} ${MAKE_ENV} ${MAKE_CMD} obj)

post-install-SOURCE-on:
		${MKDIR} ${KMODSRC}
		${INSTALL_DATA} ${WRKSRC}/Makefile ${KMODSRC}
.for dir in ${SRCDIRS}
		cd ${WRKSRC} && ${COPYTREE_SHARE} ${dir} ${KMODSRC}
.endfor

.include <bsd.port.mk>
