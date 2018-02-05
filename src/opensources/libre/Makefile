TOP         := $(CURDIR)/../../..
NAME        := re
VERSION     := 0.5.7
SOURCE      := $(NAME)-$(VERSION)
SOURCE_FILE := $(SOURCE).tar.gz
SOURCE_URL  := http://www.creytiv.com/pub/$(SOURCE_FILE)
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

OPTIONS  := \
	AR=$(AR) \
	CC=$(CC) \
	LD=$(LD) \
	RANLIB=$(RANLIB) \
	SYSROOT=/opt/Vatics/vtcs_toolchain/arm-eabi-uclibc/usr/arm-buildroot-linux-uclibcgnueabi/sysroot/usr \
	SYSROOT_ALT=$(INSTALL_PREFIX) \
	OPT_SIZE=1 \
	OPT_SPEED=1 \
	USE_OPENSSL=1 \
	USE_ZLIB=1 \
	PREFIX=$(INSTALL_PREFIX)

.PHONY: all download configure patch clean distclean install uninstall

all: patch
	make -C $(SOURCE) $(OPTIONS) || exit 1

patch: configure
	if [ ! -f $(SOURCE)/.patched ]; then \
		patch -p0 < $(PATCH_DIR)/$(SOURCE).patch \
		&& touch $(SOURCE)/.patched; \
	fi

configure: download
	if [ ! -f $(SOURCE)/.configured ]; then \
		cd $(SOURCE) \
		&& touch .configured \
		&& cd -; \
	fi

download:
	if [ ! -d $(SOURCE) ]; then \
		wget -qO- $(SOURCE_URL) | tar xvz; \
	fi

clean:
	make -C $(SOURCE) $(OPTIONS) clean || exit 1

distclean:
	rm -rf $(SOURCE)

install:
	make -C $(SOURCE) $(OPTIONS) install || exit 1

uninstall:
	make -C $(SOURCE) $(OPTIONS) uninstall || exit 1
