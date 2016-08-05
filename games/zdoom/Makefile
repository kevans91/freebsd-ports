# Created by: Kyle Evans <self@kyle-evans.net>
# $FreeBSD$

PORTNAME=	zdoom
PORTVERSION=	2.8.1
CATEGORIES=	games

MAINTAINER=	bsdports@kyle-evans.net
COMMENT=	Source port for Doom-engine games

BUILD_DEPENDS=	zip:archivers/zip
LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libsndfile.so:audio/libsndfile

PLIST_FILES=	bin/${PORTNAME} \
		%%DATADIR%%/${PORTNAME}.pk3

USE_GITHUB=	yes
GH_ACCOUNT=	rheit
GH_PROJECT=	zdoom

USES=		cmake:outsource \
		openal \
		pkgconfig \
		gettext \
		jpeg
USE_GNOME=	gtk20 \
		pango \
		atk \
		cairo \
		gdkpixbuf2
USE_SDL=	sdl2
CMAKE_ARGS+=		-DNO_FMOD:BOOL=ON
CMAKE_BUILD_TYPE?=	Release

OPTIONS_DEFINE=	FLUIDSYNTH
OPTIONS_DEFAULT=FLUIDSYNTH

FLUIDSYNTH_DESC=	FluidSynth sound library support
FLUIDSYNTH_LIB_DEPENDS=	libfluidsynth.so:audio/fluidsynth
FLUIDSYNTH_CMAKE_ON=	-DWITH_FLUIDSYNTH:BOOL=ON
FLUIDSYNTH_CMAKE_OFF=	-DWITH_FLUIDSYNTH:BOOL=OFF

.include "${.CURDIR}/../doom-data/Makefile.include"

do-install:
	@${MKDIR}	${STAGEDIR}${PREFIX}/share/${PORTNAME}
	${INSTALL_PROGRAM} ${CONFIGURE_WRKSRC}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_DATA} ${CONFIGURE_WRKSRC}/${PORTNAME}.pk3 ${STAGEDIR}${PREFIX}/share/${PORTNAME}/

.include <bsd.port.mk>
