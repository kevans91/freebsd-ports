# $FreeBSD$

PORTNAME=	BOSSA
PORTVERSION=	1.7.0.a
CATEGORIES=	devel
MAINTAINER=	bsdports@kyle-evans.net
COMMENT=	Flash programmer for Atmel SAM microcontrollers

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/LICENSE

USE_GITHUB=	yes
GH_ACCOUNT=	shumatech
GH_TAGNAME=	ae08c63

USES=		compiler:c++11-lang gmake

CXXFLAGS+=	-I${PREFIX}/include
LDFLAGS+=	-L${PREFIX}/lib

ALL_TARGET=	bin/bossac

OPTIONS_DEFINE=	BOSSA BOSSASH
OPTIONS_DEFAULT=	BOSSASH
OPTIONS_SUB=	yes

BOSSA_DESC=	Include BOSSA GUI application using wxWidgets
BOSSA_ALL_TARGET=	bin/bossa

BOSSASH_DESC=	Include BOSSA Shell
BOSSASH_USES=	readline
BOSSASH_ALL_TARGET=	bin/bossash

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossac ${STAGEDIR}${PREFIX}/bin/bossac

do-install-BOSSA-on:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossa ${STAGEDIR}${PREFIX}/bin/bossa

do-install-BOSSASH-on:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossash ${STAGEDIR}${PREFIX}/bin/bossash

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MBOSSA}
USE_WX=		3.0
WX_COMPS=	wx
.endif

post-extract:
	${REINPLACE_CMD} -e 's/wx-config/$${WX_CONFIG}/' ${WRKSRC}/Makefile

.include <bsd.port.mk>
