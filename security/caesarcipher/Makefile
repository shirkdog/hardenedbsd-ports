# $FreeBSD$

PORTNAME=	caesarcipher
PORTVERSION=	1.0
CATEGORIES=	security
MASTER_SITES=	http://www.olivermahmoudi.com/files/

MAINTAINER=	fbsd@olivermahmoudi.com
COMMENT=	Caesar cipher cryptography tool

LICENSE=	BSD2CLAUSE

PLIST_FILES=	bin/caesarcipher \
		man/man1/caesarcipher.1.gz
WRKSRC=		${WRKDIR}/${PORTNAME}

do-build:
	cd ${WRKSRC} && ${CC} ${CFLAGS} ${LDFLAGS} -o ${PORTNAME} ${PORTNAME}.c

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.1 ${STAGEDIR}${PREFIX}/man/man1

.include <bsd.port.mk>
