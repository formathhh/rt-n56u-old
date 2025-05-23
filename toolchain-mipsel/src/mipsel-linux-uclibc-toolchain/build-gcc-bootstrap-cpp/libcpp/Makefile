# Makefile.  Generated from Makefile.in by configure.
# Makefile for libcpp.  Run 'configure' to generate Makefile from Makefile.in

# Copyright (C) 2004, 2008, 2009 Free Software Foundation, Inc.

#This file is part of libcpp.

#libcpp is free software; you can redistribute it and/or modify
#it under the terms of the GNU General Public License as published by
#the Free Software Foundation; either version 3, or (at your option)
#any later version.

#libcpp is distributed in the hope that it will be useful,
#but WITHOUT ANY WARRANTY; without even the implied warranty of
#MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#GNU General Public License for more details.

#You should have received a copy of the GNU General Public License
#along with libcpp; see the file COPYING3.  If not see
#<http://www.gnu.org/licenses/>.



srcdir = ../../gcc-4.4.7/libcpp
top_builddir = .
VPATH = ../../gcc-4.4.7/libcpp
INSTALL = /usr/bin/install -c
AR = ar
ARFLAGS = cru
ACLOCAL = aclocal
AUTOCONF = autoconf
AUTOHEADER = autoheader
CATALOGS = $(patsubst %,po/%,)
CC = gcc
CFLAGS = -O2 -Wno-pointer-sign -Wno-trigraphs -Wno-format-security -Wno-unused-but-set-variable -Wno-sizeof-pointer-memaccess -fno-delete-null-pointer-checks -fgnu89-inline
WARN_CFLAGS = -W -Wall -Wwrite-strings -Wstrict-prototypes -Wmissing-prototypes -Wold-style-definition -Wmissing-format-attribute -pedantic -Wno-long-long 
CPP = gcc -E
CPPFLAGS = 
EXEEXT = 
GMSGFMT = /usr/bin/msgfmt
INCINTL = 
INSTALL_DATA = ${INSTALL} -m 644
INSTALL_PROGRAM = ${INSTALL}
INSTALL_SCRIPT = ${INSTALL}
LDFLAGS = 
LIBICONV = 
LIBINTL = 
PACKAGE = cpplib
RANLIB = ranlib
SHELL = /bin/bash
USED_CATALOGS = 
XGETTEXT = /usr/bin/xgettext
DEPMODE = depmode=gcc3
DEPDIR = .deps

datarootdir = @datarootdir@
datadir = ${prefix}/share
exec_prefix = /opt/rt-n56u/toolchain-mipsel/toolchain-3.4.x
libdir = ${exec_prefix}/lib
localedir = $(datadir)/locale
prefix = /opt/rt-n56u/toolchain-mipsel/toolchain-3.4.x

MSGMERGE = msgmerge
mkinstalldirs = $(SHELL) $(srcdir)/../mkinstalldirs
depcomp = $(SHELL) $(srcdir)/../depcomp

INCLUDES = -I$(srcdir) -I. -I$(srcdir)/../include  \
	-I$(srcdir)/include

ALL_CFLAGS = $(CFLAGS) $(WARN_CFLAGS) $(INCLUDES) $(CPPFLAGS)

libcpp_a_OBJS = charset.o directives.o directives-only.o errors.o \
	expr.o files.o identifiers.o init.o lex.o line-map.o macro.o \
	mkdeps.o pch.o symtab.o traditional.o
makedepend_OBJS = makedepend.o

libcpp_a_SOURCES = charset.c directives.c directives-only.c errors.c \
	expr.c files.c identifiers.c init.c lex.c line-map.c macro.c \
	mkdeps.c pch.c symtab.c traditional.c

all: libcpp.a makedepend$(EXEEXT) $(USED_CATALOGS)

.SUFFIXES:
.SUFFIXES: .c .gmo .o .obj .po .pox

libcpp.a: $(libcpp_a_OBJS)
	-rm -f libcpp.a
	$(AR) $(ARFLAGS) libcpp.a $(libcpp_a_OBJS)
	$(RANLIB) libcpp.a

makedepend$(EXEEXT): $(makedepend_OBJS) libcpp.a ../libiberty/libiberty.a
	@rm -f makedepend$(EXEEXT)
	$(CC) $(CFLAGS) $(LDFLAGS) -o makedepend$(EXEEXT) \
	  $(makedepend_OBJS) libcpp.a ../libiberty/libiberty.a \
	  $(LIBINTL) $(LIBICONV)

# Rules to rebuild the configuration

Makefile: $(srcdir)/Makefile.in config.status
	$(SHELL) ./config.status Makefile

config.status: $(srcdir)/configure
	$(SHELL) ./config.status --recheck

$(srcdir)/configure: # $(srcdir)/aclocal.m4
	cd $(srcdir) && $(AUTOCONF)

$(srcdir)/aclocal.m4: # $(srcdir)/../config/acx.m4 \
	$(srcdir)/../config/gettext-sister.m4 $(srcdir)/../config/iconv.m4 \
	$(srcdir)/../config/codeset.m4 $(srcdir)/../config/lib-ld.m4 \
	$(srcdir)/../config/lib-link.m4 $(srcdir)/../config/lib-prefix.m4 \
	$(srcdir)/../config/override.m4 $(srcdir)/../config/proginstall.m4 \
	$(srcdir)/configure.ac
	cd $(srcdir) && $(ACLOCAL) -I ../config

config.h: stamp-h1
	test -f config.h || (rm -f stamp-h1 && $(MAKE) stamp-h1)

stamp-h1: $(srcdir)/config.in config.status
	-rm -f stamp-h1
	$(SHELL) ./config.status config.h

$(srcdir)/config.in: # $(srcdir)/configure.ac
	cd $(srcdir) && $(AUTOHEADER)
	-rm -f stamp-h1

# It is not possible to get LOCALEDIR defined in config.h because
# the value it needs to be defined to is only determined in the
# Makefile.  Hence we do this instead.
localedir.h: localedir.hs; @true
localedir.hs: Makefile
	echo "#define LOCALEDIR \"$(localedir)\"" > localedir.new
	$(srcdir)/../move-if-change localedir.new localedir.h
	echo timestamp > localedir.hs

# Installation rules and other phony targets

# These rule has to look for .gmo modules in both srcdir and
# the cwd, and has to check that we actually have a catalog
# for each language, in case they weren't built or included
# with the distribution.
installdirs:
	@$(mkinstalldirs) $(DESTDIR)$(datadir); \
	cats="$(CATALOGS)"; for cat in $$cats; do \
	  lang=`basename $$cat | sed 's/\.gmo$$//'`; \
	  if [ -f $$cat ] || [ -f $(srcdir)/$$cat ]; then \
	    dir=$(localedir)/$$lang/LC_MESSAGES; \
	    $(mkinstalldirs) $(DESTDIR)$$dir || exit 1; \
	  fi; \
	done

install-strip install: all installdirs
	cats="$(CATALOGS)"; for cat in $$cats; do \
	  lang=`basename $$cat | sed 's/\.gmo$$//'`; \
	  if [ -f $$cat ]; then :; \
	  elif [ -f $(srcdir)/$$cat ]; then cat=$(srcdir)/$$cat; \
	  else continue; \
	  fi; \
	  dir=$(localedir)/$$lang/LC_MESSAGES; \
	  echo $(INSTALL_DATA) $$cat $(DESTDIR)$$dir/$(PACKAGE).mo; \
	  $(INSTALL_DATA) $$cat $(DESTDIR)$$dir/$(PACKAGE).mo; \
	done

mostlyclean:
	-rm -f *.o

clean: mostlyclean
	-rm -rf makedepend$(EXEEXT) libcpp.a $(srcdir)/autom4te.cache

distclean: clean
	-rm -f config.h stamp-h1 config.status config.cache config.log \
	  configure.lineno configure.status.lineno Makefile localedir.h \
	  localedir.hs $(DEPDIR)/*.Po
	-rmdir $(DEPDIR)

maintainer-clean: distclean
	@echo "This command is intended for maintainers to use"
	@echo "it deletes files that may require special tools to rebuild."
	-rm -f $(srcdir)/configure $(srcdir)/aclocal.m4

check:
installcheck:
dvi:
pdf:
html:
info:
install-info:
install-pdf:
install-man:
install-html:

update-po: $(CATALOGS:.gmo=.pox)

.PHONY: installdirs install install-strip mostlyclean clean distclean \
  maintainer-clean check installcheck dvi pdf html info install-info \
  install-man update-po install-html

# Dependency rule.
COMPILE.base = $(CC) $(DEFS) $(INCLUDES) $(CPPFLAGS) $(ALL_CFLAGS) -c
ifeq ($(DEPMODE),depmode=gcc3)
# Note that we put the dependencies into a .Tpo file, then move them
# into place if the compile succeeds.  We need this because gcc does
# not atomically write the dependency output file.
COMPILE = $(COMPILE.base) -o $@ -MT $@ -MMD -MP -MF $(DEPDIR)/$*.Tpo
POSTCOMPILE = @mv $(DEPDIR)/$*.Tpo $(DEPDIR)/$*.Po
else
COMPILE = source='$<' object='$@' libtool=no DEPDIR=$(DEPDIR) $(DEPMODE) \
	  $(depcomp) $(COMPILE.base)
# depcomp handles atomicity for us, so we don't need a postcompile
# step.
POSTCOMPILE =
endif

# Implicit rules and I18N

.c.o:
	$(COMPILE) $<
	$(POSTCOMPILE)

# N.B. We do not attempt to copy these into $(srcdir).
.po.gmo:
	$(mkinstalldirs) po
	$(GMSGFMT) --statistics -o $@ $<

# The new .po has to be gone over by hand, so we deposit it into
# build/po with a different extension.
# If build/po/$(PACKAGE).pot exists, use it (it was just created),
# else use the one in srcdir.
.po.pox:
	$(mkinstalldirs) po
	$(MSGMERGE) $< `if test -f po/$(PACKAGE).pot; \
	                then echo po/$(PACKAGE).pot; \
	                else echo $(srcdir)/po/$(PACKAGE).pot; fi` -o $@

# Rule for regenerating the message template.
$(PACKAGE).pot: po/$(PACKAGE).pot
po/$(PACKAGE).pot: $(libcpp_a_SOURCES)
	$(mkinstalldirs) $(srcdir)/po
	$(XGETTEXT) --default-domain=$(PACKAGE) \
	  --keyword=_ --keyword=N_ \
	  --keyword=cpp_error:3 --keyword=cpp_errno:3 \
	  --keyword=cpp_error_with_line:5 \
	  --keyword=SYNTAX_ERROR --keyword=SYNTAX_ERROR2 \
	  --copyright-holder="Free Software Foundation, Inc." \
	  --msgid-bugs-address="http://gcc.gnu.org/bugs.html" \
	  --language=c -o po/$(PACKAGE).pot.tmp $^
	sed 's:$(srcdir)/::g' <po/$(PACKAGE).pot.tmp >po/$(PACKAGE).pot
	rm po/$(PACKAGE).pot.tmp

TAGS_SOURCES = $(libcpp_a_SOURCES) makedepend.c internal.h ucnid.h \
    include/line-map.h include/symtab.h include/cpp-id-data.h \
    include/cpplib.h include/mkdeps.h system.h

TAGS: $(TAGS_SOURCES)
	cd $(srcdir) && etags $(TAGS_SOURCES)

# Tell versions [3.59,3.63) of GNU make to not export all variables.
# Otherwise a system limit (for SysV at least) may be exceeded.
.NOEXPORT:

# Dependencies
-include $(patsubst %.o, $(DEPDIR)/%.Po, $(libcpp_a_OBJS) $(makedepend_OBJS))

# Dependencies on generated headers have to be explicit.
init.o: localedir.h
