TOP         := $(CURDIR)/../../..
NAME        := pcre
VERSION     := 8.41
SOURCE      := $(NAME)-$(VERSION)
SOURCE_FILE := $(SOURCE).zip
SOURCE_URL  := https://ftp.pcre.org/pub/pcre/$(SOURCE_FILE)
PATCH_DIR   := $(CURDIR)/patch

INSTALL_PREFIX := $(TOP)/build
INSTALL_INCDIR := $(INSTALL_PREFIX)/include
INSTALL_LIBDIR := $(INSTALL_PREFIX)/lib
INSTALL_BINDIR := $(INSTALL_PREFIX)/bin

CROSS_COMPILE := /opt/buildroot-gcc463/usr/bin/mipsel-linux-
PLATFORM := mipsel-linux
CC       := $(CROSS_COMPILE)gcc
CPP      := $(CROSS_COMPILE)gcc -E
CXX      := $(CROSS_COMPILE)g++
AS       := $(CROSS_COMPILE)as
AR       := $(CROSS_COMPILE)ar
LD       := $(CROSS_COMPILE)ld
NM       := $(CROSS_COMPILE)nm
OBJCOPY  := $(CROSS_COMPILE)objcopy
OBJDUMP  := $(CROSS_COMPILE)objdump
RANLIB   := $(CROSS_COMPILE)ranlib
READELF  := $(CROSS_COMPILE)readelf
SIZE     := $(CROSS_COMPILE)size
STRINGS  := $(CROSS_COMPILE)strings
STRIP    := $(CROSS_COMPILE)strip

CFLAGS   := -g -O3 -Os -Wall
INCLUDES :=
LFLAGS   :=
LIBS     :=
LDLIBS   :=

.PHONY: all download configure patch clean distclean install uninstall

all: patch
	make -C $(SOURCE) || exit 1

patch: configure
	if [ ! -f $(SOURCE)/.patched ]; then \
		cd $(SOURCE) \
		&& touch .patched \
		&& cd -; \
	fi

configure: download
	if [ ! -f $(SOURCE)/.configured ]; then \
		cd $(SOURCE) \
		&& \
			AS="$(AS)" \
			AR="$(AR)" \
			CC="$(CC)" \
			CXX="$(CXX)" \
			LD="$(LD)" \
			NM="$(NM)" \
			OBJDUMP="$(OBJDUMP)" \
			RANLIB="$(RANLIB)" \
			STRIP="$(STRIP)" \
			./configure \
			--prefix=$(INSTALL_PREFIX) \
			--host=$(PLATFORM) \
			--with-sysroot=/opt/buildroot-gcc463/usr/mipsel-buildroot-linux-uclibc/sysroot \
			--disable-cpp \
		&& touch .configured \
		&& cd -; \
	fi

download:
	if [ ! -d $(SOURCE) ]; then \
		wget -qO- -O $(SOURCE_FILE) $(SOURCE_URL) \
		&& unzip $(SOURCE_FILE) \
		&& rm -rf $(SOURCE_FILE); \
	fi

clean:
	make -C $(SOURCE) clean || exit 1

distclean:
	rm -rf $(SOURCE)

install:
	make -C $(SOURCE) install || exit 1

uninstall:
	make -C $(SOURCE) uninstall || exit 1
