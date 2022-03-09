#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([liblzfse], [1.0.0], [https://github.com/lzfse/lzfse/issues], [], [https://github.com/lzfse/lzfse])
AM_INIT_AUTOMAKE([dist-bzip2 no-dist-gzip check-news])
m4_ifdef([AM_SILENT_RULES], [AM_SILENT_RULES])
AC_CONFIG_SRCDIR([src/])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])

dnl libtool versioning
# +1 : 0 : +1  == adds new functions to the interface
# +1 : 0 : 0   == changes or removes functions (changes include both
#                 changes to the signature and the semantic)
#  ? :+1 : ?   == just internal changes
# CURRENT : REVISION : AGE
LIBLZFSE_SO_VERSION=3:0:0

AC_SUBST(LIBLZFSE_SO_VERSION)

# Checks for programs.
AC_PROG_CC
AC_PROG_CXX
AM_PROG_CC_C_O
LT_INIT

# Checks for header files.
AC_CHECK_HEADERS([stdint.h stddef.h assert.h stdlib.h string.h limits.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T
AC_TYPE_UINT8_T

# Check for operating system
AC_MSG_CHECKING([for platform-specific build settings])
case ${host_os} in
  *mingw32*|*cygwin*)
    AC_MSG_RESULT([${host_os}])
    win32=true
    AC_DEFINE(WINVER, 0x0501, [minimum Windows version])
    ;;
  darwin*)
    AC_MSG_RESULT([${host_os}])
    darwin=true
    ;;
  *)
    AC_MSG_RESULT([${host_os}])
    AX_PTHREAD([], [AC_MSG_ERROR([pthread is required to build $PACKAGE_NAME])])
    AC_CHECK_LIB(pthread, [pthread_once], [], [AC_MSG_ERROR([pthread with pthread_once required to build $PACKAGE_NAME])])
    ;;
esac
AM_CONDITIONAL(WIN32, test x$win32 = xtrue)
AM_CONDITIONAL(DARWIN, test x$darwin = xtrue)

# Check if the C compiler supports __attribute__((constructor))
AC_CACHE_CHECK([wether the C compiler supports constructor/destructor attributes],
  ac_cv_attribute_constructor, [
  ac_cv_attribute_constructor=no
  AC_COMPILE_IFELSE([AC_LANG_PROGRAM(
    [[
      static void __attribute__((constructor)) test_constructor(void) {
      }
      static void __attribute__((destructor)) test_destructor(void) {
      }
    ]], [])],
    [ac_cv_attribute_constructor=yes]
  )]
)
if test "$ac_cv_attribute_constructor" = "yes"; then
  AC_DEFINE(HAVE_ATTRIBUTE_CONSTRUCTOR, 1, [Define if the C compiler supports constructor/destructor attributes])
fi

AS_COMPILER_FLAGS(GLOBAL_CFLAGS, "-Wall -Wextra -Wmissing-declarations -Wredundant-decls -Wshadow -Wpointer-arith -Wwrite-strings -Wswitch-default -Wno-unused-parameter -fsigned-char -fvisibility=hidden")
AC_SUBST(GLOBAL_CFLAGS)

case "$GLOBAL_CFLAGS" in
  *-fvisibility=hidden*)
    AC_DEFINE([HAVE_FVISIBILITY], [1], [Define if compiled with -fvisibility=hidden])
esac

# check for large file support
AC_SYS_LARGEFILE

m4_ifdef([AM_SILENT_RULES],[AM_SILENT_RULES([yes])])

AC_CONFIG_FILES([
Makefile
src/Makefile
src/liblzfse-1.0.pc
include/Makefile
tools/Makefile
])
AC_OUTPUT

echo "
Configuration for $PACKAGE $VERSION:
-------------------------------------------

  Install prefix: .........: $prefix

  Now type 'make' to build $PACKAGE $VERSION,
  and then 'make install' for installation.
"
