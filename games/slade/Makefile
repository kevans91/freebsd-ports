# Created by: Kyle Evans <self@kyle-evans.net>
# $FreeBSD$

PORTNAME=	slade
PORTVERSION=	3.1.1
DISTVERSIONSUFFIX=	_b3_unofficial
CATEGORIES=	games editors

MAINTAINER=	self@kyle-evans.net
COMMENT=	Modern editor for Doom-engine based games and source ports

LICENSE=	GPLv2

LIB_DEPENDS=	libfluidsynth.so:${PORTSDIR}/audio/fluidsynth \
		libfreeimage.so:${PORTSDIR}/graphics/freeimage \
		libftgl.so:${PORTSDIR}/graphics/ftgl \
		libsfml-system.so:${PORTSDIR}/devel/sfml \
		libsfml-audio.so:${PORTSDIR}/devel/sfml \
		libsfml-window.so:${PORTSDIR}/devel/sfml
BUILD_DEPENDS=  zip:${PORTSDIR}/archivers/zip

PLIST_FILES=	bin/slade \
		share/slade3/slade.pk3

USE_GITHUB=	yes
GH_ACCOUNT=	kevans91 #sirjuddington
GH_PROJECT=	SLADE

USES=		cmake:outsource \
		compiler:c++11-lib \
		pkgconfig

CXXFLAGS+=		-std=c++11
CMAKE_INSTALL_PREFIX?=	${PREFIX}
CMAKE_BUILD_TYPE?=	Release

USE_WX=		3.0+
WX_COMPS=	wx

.include <bsd.port.mk>
