# $FreeBSD$

PORTNAME=	BOSSA
PORTVERSION=	1.6.1
DISTVERSIONSUFFIX=	-arduino2	# -arduino
CATEGORIES=	devel

MAINTAINER=	bsdports@kyle-evans.net
COMMENT=	Flash programmer for Atmel SAM microcontrollers

LICENSE=	BSD3CLAUSE

USE_GITHUB=	yes
GH_ACCOUNT=	kevans91		#shumatech

USES=		compiler:c++11-lang gmake

CXXFLAGS+=	-I${PREFIX}/include
LDFLAGS+=	-L${PREFIX}/lib

ALL_TARGET=	bin/bossac

OPTIONS_DEFINE=	BOSSA BOSSASH
OPTIONS_DEFAULT=	BOSSASH
OPTIONS_SUB=	yes

BOSSA_DESC=	Include BOSSA GUI application using wxWidgets

BOSSASH_DESC=	Include BOSSA Shell
BOSSASH_USES=	readline

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossac ${STAGEDIR}${PREFIX}/bin/bossac

do-install-BOSSA-on:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossa ${STAGEDIR}${PREFIX}/bin/bossa

do-install-BOSSASH-on:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossash ${STAGEDIR}${PREFIX}/bin/bossash

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MBOSSA}
ALL_TARGET+=	bin/bossa
USE_WX=		3.0
WX_COMPS=	wx
.endif

.if ${PORT_OPTIONS:MBOSSASH}
ALL_TARGET+=	bin/bossash
.endif

.include <bsd.port.mk>
