# $FreeBSD$

PORTNAME=	BOSSA
PORTVERSION=	1.6.1
DISTVERSIONSUFFIX=	-arduino2	# -arduino
CATEGORIES=	devel

MAINTAINER=	bsdports@kyle-evans.net
COMMENT=	Flash programmer for Atmel SAM microcontrollers

USE_GITHUB=	yes
GH_ACCOUNT=	kevans91		#shumatech

USES=		compiler:c++11-lang \
		gmake \
		readline

USE_WX=		3.0
WX_COMPS=	wx

CXXFLAGS+=	-I/usr/local/include
LDFLAGS+=	-L/usr/local/lib

PLIST_FILES=	bin/bossa \
		bin/bossac \
		bin/bossash

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossa ${STAGEDIR}${PREFIX}/bin/bossa
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossac ${STAGEDIR}${PREFIX}/bin/bossac
	${INSTALL_PROGRAM} ${WRKSRC}/bin/bossash ${STAGEDIR}${PREFIX}/bin/bossash

.include <bsd.port.mk>
