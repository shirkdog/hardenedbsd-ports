# $FreeBSD$

PORTNAME=	binaryen
DISTVERSION=	1.38.32
PORTREVISION=	1
CATEGORIES=	devel

MAINTAINER=	greg@unrelenting.technology
COMMENT=	Compiler infrastructure and toolchain library for WebAssembly

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		cmake python:2.7,build compiler:c++11-lang
USE_GITHUB=	yes
GH_ACCOUNT=	WebAssembly
USE_LDCONFIG=	yes

BINARY_ALIAS=	python=${PYTHON_CMD}

.include <bsd.port.mk>
