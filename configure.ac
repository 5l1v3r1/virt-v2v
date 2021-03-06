# virt-v2v
# Copyright (C) 2009-2020 Red Hat Inc.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

# The major, minor, and release fields MUST be numbers.  Packagers can
# add extra information using --with-extra="..." which may be any
# freeform string.
m4_define([v2v_major],   [1])
m4_define([v2v_minor],   [41])
m4_define([v2v_release], [8])

AC_INIT([virt-v2v],v2v_major.v2v_minor.v2v_release)

# Headings within the configure script output.
m4_define([HEADING],
          [AS_ECHO
           AS_ECHO(["--- $1 ---"])])

AC_CONFIG_AUX_DIR([build-aux])

AC_USE_SYSTEM_EXTENSIONS

dnl Initialize automake.
AM_INIT_AUTOMAKE(foreign subdir-objects tar-pax) dnl NB: Do not [quote] this parameter.

m4_ifndef([AM_SILENT_RULES], [m4_define([AM_SILENT_RULES],[])])
AM_SILENT_RULES([yes]) # make --enable-silent-rules the default.

AC_CONFIG_MACRO_DIR([m4])

dnl Initialize libtool.
LT_INIT

dnl Extra string, a freeform string defined by packagers.
AC_ARG_WITH([extra],
    [AS_HELP_STRING([--with-extra],
                    [extra version string (for use by packagers)])],
    [v2v_extra="$withval"],
    [v2v_extra=]
)

AC_MSG_NOTICE([virt-v2v version v2v_major.v2v_minor.v2v_release$v2v_extra])

dnl Split up the version string.
AC_DEFINE([PACKAGE_VERSION_MAJOR],[v2v_major],[Major version number.])
AC_DEFINE([PACKAGE_VERSION_MINOR],[v2v_minor],[Minor version number.])
AC_DEFINE([PACKAGE_VERSION_RELEASE],[v2v_release],[Release number.])
AC_DEFINE_UNQUOTED([PACKAGE_VERSION_EXTRA],["$v2v_extra"],[Extra version string.])
PACKAGE_VERSION_FULL="v2v_major.v2v_minor.v2v_release${v2v_extra}"
AC_DEFINE_UNQUOTED([PACKAGE_VERSION_FULL],["$PACKAGE_VERSION_FULL"],[Full version string.])
AC_SUBST([PACKAGE_VERSION_FULL])

dnl Early gnulib initialization.
HEADING([Configuring Gnulib])
gl_EARLY
gl_INIT

dnl Check for external programs required to either build or run
dnl virt-v2v.
HEADING([Checking for external programs])
m4_include([m4/guestfs-progs.m4])

dnl The C compiler environment.
HEADING([Checking for the C compiler environment])
m4_include([m4/guestfs-c.m4])

dnl Any C libraries required by virt-v2v.
HEADING([Checking for libraries used by virt-v2v])
m4_include([m4/guestfs-libraries.m4])

dnl OCaml.
HEADING([Checking for OCaml])
m4_include([m4/guestfs-ocaml.m4])

dnl Perl, used for running mllibvirt generator, and man pages.
HEADING([Checking for Perl])
m4_include([m4/guestfs-perl.m4])

dnl virt-v2v.
HEADING([Checking the virt-v2v dependencies])
m4_include([m4/guestfs-v2v.m4])

dnl Bash completion.
HEADING([Checking for bash completion])
m4_include([m4/guestfs-bash-completion.m4])

dnl These are required to get common/*/Makefile.am files
dnl to work.  We should further decouple these in future XXX
AM_CONDITIONAL([ENABLE_APPLIANCE],[true])
AM_CONDITIONAL([HAVE_PYTHON],[false])  dnl Disables a test

dnl Produce output files.
HEADING([Generating output files])

AC_CONFIG_HEADERS([config.h])

AC_CONFIG_FILES([installcheck.sh],
                [chmod +x,-w installcheck.sh])
AC_CONFIG_FILES([ocaml-dep.sh],
                [chmod +x,-w ocaml-dep.sh])
AC_CONFIG_FILES([ocaml-link.sh],
                [chmod +x,-w ocaml-link.sh])
AC_CONFIG_FILES([podwrapper.pl],
                [chmod +x,-w podwrapper.pl])
AC_CONFIG_FILES([run],
                [chmod +x,-w run])

dnl NB: Remove common/mlstdutils/guestfs_config.ml in future XXX
AC_CONFIG_FILES([Makefile
                 bash/Makefile
                 bundled/libvirt-ocaml/Makefile
                 common/options/Makefile
                 common/mlcustomize/Makefile
                 common/mlgettext/Makefile
                 common/mlpcre/Makefile
                 common/mlstdutils/Makefile
                 common/mlstdutils/guestfs_config.ml
                 common/mltools/Makefile
                 common/mlutils/Makefile
                 common/mlv2v/Makefile
                 common/mlxml/Makefile
                 common/qemuopts/Makefile
                 common/utils/Makefile
                 config.sh
                 docs/Makefile
                 gnulib/lib/Makefile
                 gnulib/tests/Makefile
                 po-docs/Makefile
                 po-docs/ja/Makefile
                 po-docs/uk/Makefile
                 po/Makefile
                 test-data/Makefile
                 test-data/binaries/Makefile
                 test-data/blank-disks/Makefile
                 test-data/fake-virtio-win/Makefile
                 test-data/fake-virt-tools/Makefile
                 test-data/files/Makefile
                 test-data/phony-guests/Makefile
                 test-data/phony-guests/guests.xml
                 test-harness/Makefile
                 test-harness/META
                 tests/Makefile
                 v2v/Makefile
                 v2v/config.ml])

AC_OUTPUT

dnl Produce summary.
echo
echo
echo "------------------------------------------------------------"
echo "Thank you for downloading $PACKAGE_STRING"
echo
echo "Please report bugs back to the mailing list:"
echo "http://www.redhat.com/mailman/listinfo/libguestfs"
echo
echo "Next you should type 'make' to build the package,"
echo "then 'make check' to run the tests."
echo
echo "Or run 'make help' to list some common targets."
echo "------------------------------------------------------------"
