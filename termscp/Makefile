# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=termscp
PKG_VERSION:=1.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/veeso/termscp/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=cf3570c396ba36987059729f2704a88b87e4f154914062cf390b038694496be9

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += \
	chrono-0444 getrandom-0217 getrandom-034 getrandom-042 \
	iana-time-zone-0164 nucleo-050

define Package/termscp
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=File Transfer
  TITLE:=a feature rich terminal file transfer and explorer
  URL:=https://termscp.veeso.dev
  DEPENDS:=+libdbus +libopenssl +zlib
endef

define Package/termscp/description
  termscp is a feature rich terminal file transfer and explorer with
  support for SCP/SFTP/FTP/S3.
endef

# all: samba4-dev
#	error: failed to run custom build command for `pavao v0.2.3`
#	error: could not find system library 'smbclient' required by the 'pavao' crate
CARGO_ARGS += --no-default-features --features keyring

# error: failed to run custom build command for `openssl-sys v0.9.108`
RUSTC_VARS += OPENSSL_NO_VENDOR=1

# x86_64: undefined reference to `__stack_chk_guard'
ifeq ($(CONFIG_x86_64),y)
PKG_RUSTFLAGS += $(if $(CONFIG_GCC_LIBSSP),-l dylib=ssp) -C relocation-model=pic
endif

define Package/termscp/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/termscp $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,termscp))
