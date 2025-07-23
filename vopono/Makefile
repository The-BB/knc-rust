# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=vopono
PKG_VERSION:=0.10.12
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/jamesmcm/vopono/tar.gz/refs/tags/$(PKG_VERSION)?
PKG_HASH:=86e7a0a3990e605b9f5cc5bffa0741558ac88bdb8f5da83fb36ac3653f8fac5f

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0437 getrandom-0216 getrandom-033 iana-time-zone-0160

define Package/vopono
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=Run applications through VPN tunnels
  URL:=https://github.com/jamesmcm/vopono
  DEPENDS:=+liblzma
endef

define Package/vopono/description
  Launch applications via VPN tunnels using temporary network namespaces.
endef

define Package/vopono/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/vopono $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,vopono))
