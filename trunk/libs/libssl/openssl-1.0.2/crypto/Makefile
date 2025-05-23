#
# OpenSSL/crypto/Makefile
#

DIR=		crypto
TOP=		..
CC=		cc
INCLUDE=	-I. -I$(TOP) -I../include $(ZLIB_INCLUDE)
# INCLUDES targets sudbirs!
INCLUDES=	-I.. -I../.. -I../modes -I../asn1 -I../evp -I../../include $(ZLIB_INCLUDE)
CFLAG=		-g
MAKEDEPPROG=	makedepend
MAKEDEPEND=	$(TOP)/util/domd $(TOP) -MD $(MAKEDEPPROG)
MAKEFILE=       Makefile
RM=             rm -f
AR=		ar r

RECURSIVE_MAKE=	[ -n "$(SDIRS)" ] && for i in $(SDIRS) ; do \
		    (cd $$i && echo "making $$target in $(DIR)/$$i..." && \
		    $(MAKE) -e TOP=../.. DIR=$$i INCLUDES='$(INCLUDES)' $$target ) || exit 1; \
		done;

PEX_LIBS=
EX_LIBS=
 
CFLAGS= $(INCLUDE) $(CFLAG)
ASFLAGS= $(INCLUDE) $(ASFLAG)
AFLAGS=$(ASFLAGS)
CPUID_OBJ=mem_clr.o

LIBS=

GENERAL=Makefile README crypto-lib.com install.com
TEST=constant_time_test.c

LIB= $(TOP)/libcrypto.a
SHARED_LIB= libcrypto$(SHLIB_EXT)
LIBSRC=	cryptlib.c mem.c mem_clr.c mem_dbg.c cversion.c ex_data.c cpt_err.c \
	ebcdic.c uid.c o_time.c o_str.c o_dir.c o_fips.c o_init.c fips_ers.c \
	getenv.c
LIBOBJ= cryptlib.o mem.o mem_dbg.o cversion.o ex_data.o cpt_err.o ebcdic.o \
	uid.o o_time.o o_str.o o_dir.o o_fips.o o_init.o fips_ers.o getenv.o \
	$(CPUID_OBJ)

SRC= $(LIBSRC)

EXHEADER= crypto.h opensslv.h opensslconf.h ebcdic.h symhacks.h \
	ossl_typ.h
HEADER=	cryptlib.h buildinf.h md32_common.h o_time.h o_str.h o_dir.h \
	constant_time_locl.h bn_int.h $(EXHEADER)

ALL=    $(GENERAL) $(SRC) $(HEADER)

top:
	@(cd ..; $(MAKE) DIRS=$(DIR) all)

all: shared

buildinf.h: ../Makefile
	$(PERL) $(TOP)/util/mkbuildinf.pl "$(CC) $(CFLAGS)" "$(PLATFORM)" >buildinf.h

x86cpuid.s:	x86cpuid.pl perlasm/x86asm.pl
	$(PERL) x86cpuid.pl $(PERLASM_SCHEME) $(CFLAGS) $(PROCESSOR) > $@

applink.o:	$(TOP)/ms/applink.c
	$(CC) $(CFLAGS) -c -o $@ $(TOP)/ms/applink.c

uplink.o:	$(TOP)/ms/uplink.c applink.o
	$(CC) $(CFLAGS) -c -o $@ $(TOP)/ms/uplink.c

uplink-x86.s:	$(TOP)/ms/uplink-x86.pl
	$(PERL) $(TOP)/ms/uplink-x86.pl $(PERLASM_SCHEME) > $@

x86_64cpuid.s: x86_64cpuid.pl;	$(PERL) x86_64cpuid.pl $(PERLASM_SCHEME) > $@
ia64cpuid.s: ia64cpuid.S;	$(CC) $(CFLAGS) -E ia64cpuid.S > $@
ppccpuid.s:	ppccpuid.pl;	$(PERL) ppccpuid.pl $(PERLASM_SCHEME) $@
pariscid.s:	pariscid.pl;	$(PERL) pariscid.pl $(PERLASM_SCHEME) $@
alphacpuid.s:	alphacpuid.pl
	(preproc=$$$$.$@.S; trap "rm $$preproc" INT; \
	$(PERL) alphacpuid.pl > $$preproc && \
	$(CC) -E -P $$preproc > $@ && rm $$preproc)

testapps:
	[ -z "$(THIS)" ] || (	if echo $(SDIRS) | fgrep ' des '; \
				then cd des && $(MAKE) -e des; fi )
	[ -z "$(THIS)" ] || ( cd pkcs7 && $(MAKE) -e testapps );
	@if [ -z "$(THIS)" ]; then $(MAKE) -f $(TOP)/Makefile reflect THIS=$@; fi

subdirs:
	+@target=all; $(RECURSIVE_MAKE)

files:
	$(PERL) $(TOP)/util/files.pl "CPUID_OBJ=$(CPUID_OBJ)" Makefile >> $(TOP)/MINFO
	+@target=files; $(RECURSIVE_MAKE)

links:
	@$(PERL) $(TOP)/util/mklink.pl ../include/openssl $(EXHEADER)
	@$(PERL) $(TOP)/util/mklink.pl ../test $(TEST)
	@$(PERL) $(TOP)/util/mklink.pl ../apps $(APPS)
	@target=links; $(RECURSIVE_MAKE)

# lib: $(LIB): are splitted to avoid end-less loop
lib:	$(LIB)
	@touch lib
$(LIB):	$(LIBOBJ) | subdirs
	$(AR) $(LIB) $(LIBOBJ)
	test -z "$(FIPSLIBDIR)" || $(AR) $(LIB) $(FIPSLIBDIR)fipscanister.o
	$(RANLIB) $(LIB) || echo Never mind.

shared: buildinf.h lib subdirs
	if [ -n "$(SHARED_LIBS)" ]; then \
		(cd ..; $(MAKE) $(SHARED_LIB)); \
	fi

libs:
	+@target=lib; $(RECURSIVE_MAKE)

install:
	@[ -n "$(INSTALLTOP)" ] # should be set by top Makefile...
	@headerlist="$(EXHEADER)"; for i in $$headerlist ;\
	do \
	(cp $$i $(INSTALL_PREFIX)$(INSTALLTOP)/include/openssl/$$i; \
	chmod 644 $(INSTALL_PREFIX)$(INSTALLTOP)/include/openssl/$$i ); \
	done;
	+@target=install; $(RECURSIVE_MAKE)

lint:
	@target=lint; $(RECURSIVE_MAKE)

update: local_depend
	@[ -z "$(THIS)" ] || (set -e; target=update; $(RECURSIVE_MAKE) )
	@if [ -z "$(THIS)" ]; then $(MAKE) -f $(TOP)/Makefile reflect THIS=$@; fi

depend: local_depend
	@[ -z "$(THIS)" ] || (set -e; target=depend; $(RECURSIVE_MAKE) )
	@if [ -z "$(THIS)" ]; then $(MAKE) -f $(TOP)/Makefile reflect THIS=$@; fi
local_depend:
	@[ -z "$(THIS)" -o -f buildinf.h ] || touch buildinf.h # fake buildinf.h if it does not exist
	@[ -z "$(THIS)" ] || $(MAKEDEPEND) -- $(CFLAG) $(INCLUDE) $(DEPFLAG) -- $(PROGS) $(LIBSRC)
	@[ -z "$(THIS)" -o -s buildinf.h ] || rm buildinf.h

clean:
	rm -f buildinf.h *.s *.o */*.o *.obj lib tags core .pure .nfs* *.old *.bak fluff
	@target=clean; $(RECURSIVE_MAKE)

dclean:
	$(PERL) -pe 'if (/^# DO NOT DELETE THIS LINE/) {print; exit(0);}' $(MAKEFILE) >Makefile.new
	mv -f Makefile.new $(MAKEFILE)
	rm -f opensslconf.h
	@target=dclean; $(RECURSIVE_MAKE)

# DO NOT DELETE THIS LINE -- make depend depends on it.

cpt_err.o: cpt_err.c
cryptlib.o: ../e_os.h cryptlib.c cryptlib.h
cversion.o: ../e_os.h buildinf.h cryptlib.h cversion.c
ebcdic.o: ebcdic.c
ex_data.o: ../e_os.h cryptlib.h ex_data.c
fips_ers.o: fips_ers.c
getenv.o: ../e_os.h cryptlib.h getenv.c
mem.o: ../e_os.h cryptlib.h mem.c
mem_clr.o: mem_clr.c
mem_dbg.o: ../e_os.h cryptlib.h mem_dbg.c
o_dir.o: ../e_os.h LPdir_unix.c o_dir.c o_dir.h
o_fips.o: ../e_os.h cryptlib.h o_fips.c
o_init.o: ../e_os.h o_init.c
o_str.o: ../e_os.h o_str.c o_str.h
o_time.o: o_time.c o_time.h
uid.o: uid.c
