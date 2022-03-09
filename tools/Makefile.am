AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)

AM_CFLAGS = \
	$(GLOBAL_CFLAGS) \
	$(LFS_CFLAGS)
AM_LDFLAGS = 

bin_PROGRAMS = lzfse

lzfse_SOURCES = lzfse_main.c
lzfse_CFLAGS = $(AM_CFLAGS)
lzfse_LDFLAGS = $(AM_LDFLAGS)
lzfse_LDADD = $(top_builddir)/src/liblzfse-1.0.la
