# Created by: Kyle Evans <self@kyle-evans.net>
# $FreeBSD$

PORTNAME=	zdoom
PORTVERSION=	2.8.0
DISTVERSIONPREFIX=	v
DISTVERSIONSUFFIX=	_2_unofficial
CATEGORIES=	games

MAINTAINER=	self@kyle-evans.net
COMMENT=	Source port for Doom-engine games

BUILD_DEPENDS=	zip:${PORTSDIR}/archivers/zip

PLIST_FILES=	bin/${PORTNAME} \
		share/${PORTNAME}/${PORTNAME}.pk3

USE_GITHUB=	yes
GH_ACCOUNT=	kevans91
GH_PROJECT=	zdoom

USES=		cmake:outsource \
		openal \
		pkgconfig
USE_SDL=	sdl2
CMAKE_ARGS+=		-DNO_FMOD:BOOL=ON
CMAKE_BUILD_TYPE?=	Release

OPTIONS_DEFINE=	FLUIDSYNTH
OPTIONS_DEFAULT=FLUIDSYNTH

FLUIDSYNTH_DESC=	FluidSynth sound library support
FLUIDSYNTH_LIB_DEPENDS=	libfluidsynth.so:${PORTSDIR}/audio/fluidsynth
FLUIDSYNTH_CMAKE_ON=	-DWITH_FLUIDSYNTH:BOOL=ON
FLUIDSYNTH_CMAKE_OFF=	-DWITH_FLUIDSYNTH:BOOL=OFF

do-install:
	@${MKDIR}	${STAGEDIR}${PREFIX}/share/${PORTNAME}
	${INSTALL_PROGRAM} ${CONFIGURE_WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_DATA} ${CONFIGURE_WRKSRC}/${PORTNAME}.pk3 ${STAGEDIR}${PREFIX}/share/${PORTNAME}/

.include <bsd.port.mk>
