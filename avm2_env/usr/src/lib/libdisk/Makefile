# $FreeBSD: src/lib/libdisk/Makefile,v 1.48.10.1.6.1 2010/12/21 17:09:25 kensmith Exp $

.if ${MACHINE_ARCH} == "ia64"
_open_disk=	open_ia64_disk.c
.else
_change	=	change.c
_open_disk=	open_disk.c
.endif

LIB=	disk
SRCS=	blocks.c ${_change} chunk.c create_chunk.c disk.c ${_open_disk} \
	rules.c write_disk.c 
.if ${MACHINE} == "sun4v"
SRCS+=  write_sparc64_disk.c
.else
SRCS+=  write_${MACHINE}_disk.c
.endif

INCS=	libdisk.h

WARNS?=	2

CFLAGS+=	-I${.CURDIR}/../../sys/geom

.if ${MACHINE} == "pc98"
CFLAGS+=	-DPC98
.endif

CLEANFILES+=	tmp.c tst01 tst01.o
NO_PROFILE=
NO_PIC=

MAN=		libdisk.3

.include <bsd.lib.mk>

tst01: tst01.o libdisk.a
	cc ${CFLAGS} -static tst01.o -o tst01 libdisk.a

ad0:	all install tst01
	./tst01 ad0

da0:	all install tst01
	./tst01 da0

da1:	all install tst01
	./tst01 da1
