AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)

AM_CFLAGS = \
	$(GLOBAL_CFLAGS) \
	$(LFS_CFLAGS) \
	$(PTHREAD_CFLAGS)

AM_LDFLAGS = \
	$(GLOBAL_LDFLAGS)  \
	$(PTHREAD_LIBS)

lib_LTLIBRARIES = liblzfse.la
liblzfse_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(LIBLZFSE_SO_VERSION) -no-undefined
liblzfse_la_SOURCES = \
	lzfse_decode.c lzfse_tunables.h \
	lzfse_decode_base.c lzfse_internal.h \
	lzfse_encode.c lzfse_encode_tables.h \
	lzfse_encode_base.c \
	lzfse_fse.c lzfse_fse.h \
	lzvn_decode_base.c lzvn_decode_base.h \
	lzvn_encode_base.c lzvn_encode_base.h
	
if WIN32
liblzfse_la_LDFLAGS += -avoid-version
endif

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = liblzfse.pc
