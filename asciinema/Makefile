# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2011-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=asciinema
PKG_VERSION:=3.2.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/asciinema/asciinema/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=247c7c87481f38d7788c1fb1be12021c778676c0d0ab37e529ec528f87f487ce

PKG_MAINTAINER:=Entware team, https://entware.net
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += getrandom-0216 getrandom-033

define Package/asciinema
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Terminal
  TITLE:=Terminal session recorder, streamer, and player
  URL:=https://asciinema.org
endef

define Package/asciinema/description
 Terminal session recorder, streamer, and player.
endef

define Package/asciinema/conffiles
/opt/etc/asciinema/config.toml
endef

define Package/asciinema/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/asciinema $(1)/opt/usr/bin
	$(INSTALL_DIR) $(1)/opt/etc/asciinema
	$(INSTALL_DATA) ./files/config.toml $(1)/opt/etc/asciinema
endef

$(eval $(call BuildPackage,asciinema))
