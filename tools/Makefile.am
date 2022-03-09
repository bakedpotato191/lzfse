AM_CFLAGS = $(GLOBAL_CFLAGS)  $(LFS_CFLAGS) -I$(top_srcdir)/include
AM_LDFLAGS =

bin_PROGRAMS = lzfse

lzfse_SOURCES = lzfse_main.c
lzfse_CFLAGS = $(AM_CFLAGS)
lzfse_LDFLAGS = $(AM_LDFLAGS)
lzfse_LDADD = $(top_builddir)/src/liblzfse.la
