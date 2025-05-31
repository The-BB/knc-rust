# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-explore
PKG_VERSION:=0.102.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=fa5ab698463489bfc782077915f636661712a217
PKG_SOURCE_URL:=https://github.com/amtoine/nu_plugin_explore
PKG_MIRROR_HASH:=777b6fd98df74bd5741fb7beca772c0a8c69d903693f73ad763b01090ec15d1f

PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0215 iana-time-zone-0161

define Package/nu-plugin-explore
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=A fast structured data explorer for Nushell
  URL:=https://github.com/amtoine/nu_plugin_explore
  DEPENDS:=+nushell
endef

define Package/nu-plugin-explore/description
  A fast interactive explorer tool for structured data inspired by
  nu-explore.
endef

define Package/nu-plugin-explore/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_explore \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-explore/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_explore"
endef

$(eval $(call BuildPackage,nu-plugin-explore))
