# Created by: chinsan <chinsan.tw@gmail.com>
# $FreeBSD$

PORTNAME=	lilurl
PORTVERSION=	0.1.1
PORTREVISION=	1
CATEGORIES=	www
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${PORTNAME}-${PORTVERSION}.tar.gz

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Simple PHP/MySQL script for generating lil? URLs

BROKEN_powerpc64=	Does not build

USE_PHP=	mysql pcre
NO_BUILD=	yes
NO_ARCH=	yes
WANT_PHP_WEB=	yes

WRKSRC=		${WRKDIR}/${PORTNAME}
LILURL_DIR?=	www/lilurl
PKGMESSAGE=	${WRKDIR}/pkg-message
SUB_FILES=	pkg-message
PLIST=		${WRKDIR}/pkg-plist

post-extract:
	@${MV} ${WRKSRC}/includes/conf.php ${WRKSRC}/includes/conf.php.sample

pre-install:
	@${ECHO_CMD} -e "@owner ${WWWOWN}\n@group ${WWWGRP}" > ${PLIST}
	@cd ${WRKSRC} && ${FIND} -s . -type f | \
		${SED} -e 's|^./||;s|^|${LILURL_DIR}/|' >> ${PLIST} \
		&& ${FIND} -d * -type d | \
		${SED} -e 's|^|@dir ${LILURL_DIR}/|' >> ${PLIST} \
		&& ${ECHO_CMD} @dir ${LILURL_DIR} >> ${PLIST}
	@${ECHO_CMD} -e "@owner\n@group" >> ${PLIST}

do-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/${LILURL_DIR}
	@${CP} -R ${WRKSRC}/ ${STAGEDIR}${PREFIX}/${LILURL_DIR}

post-install:
	@${SED} -e 's,%%PREFIX%%,${PREFIX},; s,%%LILURL_DIR%%,${LILURL_DIR},g' \
		${PKGMESSAGE}

.include <bsd.port.mk>
