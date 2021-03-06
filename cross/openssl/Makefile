PKG_NAME = openssl
OLD_VERSION = 1.0.2
PATCH_VERS = u
PKG_VERS = $(OLD_VERSION)$(PATCH_VERS)
PKG_EXT = tar.gz
PKG_DIST_NAME = $(PKG_NAME)-$(PKG_VERS).$(PKG_EXT)
PKG_DIST_SITE = https://www.openssl.org/source/old/$(OLD_VERSION)/
PKG_DIR = $(PKG_NAME)-$(PKG_VERS)

DEPENDS = cross/zlib

HOMEPAGE = http://www.openssl.org
COMMENT  = Compression Library
LICENSE  = http://www.openssl.org/source/license.html

CONFIGURE_TARGET = openssl_configure

INSTALL_TARGET = openssl_install

STAGING_INSTALL_PREFIX := $(INSTALL_DIR)

include ../../mk/spksrc.cross-cc.mk

OPENSSL_ARCH =
ifeq ($(findstring $(ARCH),$(x64_ARCHES)),$(ARCH))
OPENSSL_ARCH = linux-x86_64
endif
ifeq ($(findstring $(ARCH),$(x86_ARCHES)),$(ARCH))
OPENSSL_ARCH = linux-generic32
endif
ifeq ($(findstring $(ARCH),$(ARM5_ARCHES)),$(ARCH))
OPENSSL_ARCH = synology-armle
endif
ifeq ($(findstring $(ARCH),$(ARM7_ARCHES)),$(ARCH))
OPENSSL_ARCH = linux-generic32
endif
ifeq ($(findstring $(ARCH),$(ARM8_ARCHES)),$(ARCH))
OPENSSL_ARCH = linux-aarch64
endif
ifeq ($(findstring $(ARCH), powerpc),$(ARCH))
OPENSSL_ARCH = synology-ppc
endif
# TODO: validate the best OPENSSL_ARCH for the following archs:
ifeq ($(findstring $(ARCH), ppc824x ppc853x ppc854x qoriq),$(ARCH))
OPENSSL_ARCH = linux-generic32
endif
ifeq ($(strip $(OPENSSL_ARCH)),)
# unexpected arch. Please add arch to mk/spksrc.common.mk
$(error Arch $(ARCH) not expected yet)
endif


.PHONY: openssl_configure
openssl_configure:
	$(RUN) ./Configure --openssldir=/etc/ssl --prefix=$(INSTALL_PREFIX) $(OPENSSL_ARCH) zlib-dynamic shared threads

.PHONY: openssl_install
openssl_install:
	$(RUN) $(MAKE) install_sw DESTDIR=$(INSTALL_DIR)
