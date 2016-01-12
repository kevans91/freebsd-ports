# Created by: Kyle Evans <self@kyle-evans.net>
# $FreeBSD$

PORTNAME=	zdoom
PORTVERSION=	2.8.0
DISTVERSIONPREFIX=	v
DISTVERSIONSUFFIX=	_unofficial
CATEGORIES=	games

MAINTAINER=	self@kyle-evans.net
COMMENT=	Source port for Doom-engine games

#LICENSE=

LIB_DEPENDS=	libopenal.so:${PORTSDIR}/audio/openal-soft \
		libSDL2.so:${PORTSDIR}/devel/sdl20
BUILD_DEPENDS=  zip:${PORTSDIR}/archivers/zip

PLIST_FILES=	bin/zdoom \
		share/zdoom/zdoom.pk3

USE_GITHUB=	yes
GH_ACCOUNT=	kevans91 #sirjuddington
GH_PROJECT=	zdoom

USES=		cmake:outsource \
		pkgconfig

CMAKE_ARGS=		-DCMAKE_INSTALL_PREFIX=${PREFIX} \
			-DNO_FMOD=ON
CMAKE_BUILD_TYPE=	Release

.include <bsd.port.mk>
