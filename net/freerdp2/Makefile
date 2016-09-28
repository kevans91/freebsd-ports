# Created by: Alexander Logvinov <avl@FreeBSD.org>
# $FreeBSD: head/net/freerdp/Makefile 412348 2016-04-01 14:17:44Z mat $

PORTNAME=	freerdp2
PORTVERSION=	2.0.0.a
CATEGORIES=	net comms ipv6

MAINTAINER=	bsdports@kyle-evans.net
COMMENT=	Free implementation of Remote Desktop Protocol

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USE_LDCONFIG=	yes
USE_GNOME=	glib20
USES=		alias cmake:outsource cpe execinfo pkgconfig compiler:c++11-lib gettext ssl
USE_GITHUB=	yes
GH_ACCOUNT=	FreeRDP
GH_PROJECT=	${GH_ACCOUNT}
GH_TAGNAME=	1855e36

CPE_VENDOR=	freerdp_project

CMAKE_ARGS=	-DWITH_LIBSYSTEMD=OFF -DWITH_WAYLAND=OFF -DWITH_GSTREAMER_0_10=OFF
LDFLAGS+=	-L${LOCALBASE}/lib
CFLAGS+=	-I${WRKSRC}/include -I${WRKSRC}/winpr/include -I${LOCALBASE}/include

OPTIONS_DEFINE=		ALSA CUPS FFMPEG GSTREAMER PULSEAUDIO SSE X11
OPTIONS_DEFAULT=	CUPS GSTREAMER X11
OPTIONS_SUB=		yes

ALSA_LIB_DEPENDS=	libasound.so:audio/alsa-lib
ALSA_CMAKE_BOOL=	WITH_ALSA

CUPS_LIB_DEPENDS=	libcups.so:print/cups
CUPS_CMAKE_BOOL=	WITH_CUPS

FFMPEG_LIB_DEPENDS=	libavcodec.so:multimedia/ffmpeg \
			libavutil.so:multimedia/ffmpeg
FFMPEG_CMAKE_BOOL=	WITH_FFMPEG

GSTREAMER_CMAKE_BOOL=	WITH_GSTREAMER_1_0
GSTREAMER_USE=		gstreamer1=yes xorg=x11,xextproto,xext,xrandr

PULSEAUDIO_LIB_DEPENDS=	libpulse.so:audio/pulseaudio
PULSEAUDIO_CMAKE_BOOL=	WITH_PULSE

SSE_CMAKE_BOOL=		WITH_SSE2

X11_DESC=		Build FreeRDP X11 client
X11_BUILD_DEPENDS=	xmlto:textproc/xmlto
X11_CMAKE_ON=		-DWITH_XKBDFILE=OFF
X11_CMAKE_BOOL=		WITH_X11
X11_USE=		xorg=x11,xkbfile,xcursor,xextproto,xv,xinerama,xext,xcursor,xrandr,xi,xfixes,xrender

.include <bsd.port.options.mk>

post-extract:
	@${FIND} ${WRKSRC}/ -name 'CMakeLists.txt' | ${XARGS} \
		${REINPLACE_CMD} \
				-e 's|$${CMAKE_INSTALL_LIBDIR}/pkgconfig|libdata/pkgconfig|' \
				-e 's|list(APPEND $${MODULE_PREFIX}_LIBS freerdp)|list(APPEND $${MODULE_PREFIX}_LIBS freerdp2)|' \
				-e 's|list(APPEND $${MODULE_PREFIX}_LIBS winpr)|list(APPEND $${MODULE_PREFIX}_LIBS winpr2)|'
	@${FIND} ${WRKSRC}/ -name 'CMakeLists.txt' | ${XARGS} \
		${REINPLACE_CMD} -E \
				-e 's|freerdp winpr|freerdp2 winpr2|' \
				-e 's|winpr freerdp|winpr2 freerdp2|' \
				-e 's|^([[:blank:]]*)target_link_libraries\((.+) freerdp\)([[:blank:]]*)$$|\1target_link_libraries(\2 freerdp2)\3|' \
				-e 's|^([[:blank:]]*)target_link_libraries\((.+) winpr\)([[:blank:]]*)$$|\1target_link_libraries(\2 winpr2)\3|' \
				-e 's|^([[:blank:]]*)set\((.+) freerdp (.+) winpr\)([[:blank:]]*)$$|\1set(\2 freerdp2 \3 winpr2)\4|' \
				-e 's|^([[:blank:]]*)set\((.+) winpr\)([[:blank:]]*)$$|\1set(\2 winpr2)\3|'
	@${REINPLACE_CMD} -e '/CMAKE_INSTALL_RPATH /d' \
		${WRKSRC}/CMakeLists.txt
	@${REINPLACE_CMD} -e 's/OPENBSD/OPENBSD OR FREEBSD/' \
		${WRKSRC}/winpr/CMakeLists.txt \
		${WRKSRC}/client/X11/CMakeLists.txt
	@${REINPLACE_CMD} -e 's/NetBSD__)/NetBSD__) || defined(__FreeBSD__)/' \
		${WRKSRC}/winpr/libwinpr/utils/trio/triodef.h
	@${REINPLACE_CMD} -e 's|<malloc.h>|<stdlib.h>|' \
		${WRKSRC}/channels/drive/client/statvfs.c
	@${RM} ${WRKSRC}/cmake/FindOpenSSL.cmake

.include <bsd.port.mk>
