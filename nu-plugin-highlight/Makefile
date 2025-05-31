# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-highlight
PKG_VERSION:=1.4.5
PKG_RELEASE:=1

NU_VERSION:=0.104.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)+$(NU_VERSION)
PKG_SOURCE_URL:=https://github.com/cptpiepmatz/nu-plugin-highlight
PKG_MIRROR_HASH:=2055d326f8c4282ed742fc30fffbaf9b7b1a5a9e5290430ac7a3fda56e603c94

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0216 iana-time-zone-0163

define Package/nu-plugin-highlight
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=nu plugin for syntax highlighting
  URL:=https://github.com/cptpiepmatz/nu-plugin-highlight
  DEPENDS:=+nushell
endef

define Package/nu-plugin-highlight/description
  nu-plugin-highlight is a plugin for Nushell that provides
  syntax highlighting for source code.
endef

define Package/nu-plugin-highlight/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_highlight \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-highlight/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_highlight"
endef

$(eval $(call BuildPackage,nu-plugin-highlight))
