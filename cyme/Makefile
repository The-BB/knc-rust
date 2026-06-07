# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=cyme
PKG_VERSION:=3.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/tuna-f1sh/cyme/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=bd73a4b6f9fe502d140c9d5d3c972d85dccb53f4222afeb8260e97f1f95b96b0

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0444 getrandom-0217 iana-time-zone-0164

define Package/cyme
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=List system USB buses and devices
  URL:=https://github.com/tuna-f1sh/cyme
  DEPENDS:=+libusb-1.0 @!(USE_MUSL&&(mips||mipsel))
endef

define Package/cyme/description
  List system USB buses and devices; a lib and modern cross-platform
  lsusb that attempts to maintain compatibility with, but also add new features.
endef

define Package/cyme/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cyme $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,cyme))
