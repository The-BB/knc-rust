# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=vopono
PKG_VERSION:=0.10.18
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/jamesmcm/vopono/tar.gz/$(PKG_VERSION)?
PKG_HASH:=3b2c1d185af1065d61fc6cc9f90ba942d0134a3256e93713633640b600373b05

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Entware team, https://entware.net

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += \
	chrono-0444 getrandom-0217 getrandom-034 getrandom-042 iana-time-zone-0164

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
