# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-port-extension
PKG_VERSION:=0.104.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=c859f28b9d9fd99333fecafa26c97bf32565282b
PKG_SOURCE_URL:=https://github.com/FMotalleb/nu_plugin_port_extension
PKG_MIRROR_HASH:=7e29aee31525baab84d4b82d7b1810b23bf66d48f5214df0f0fe4ca1fa0b2114

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0216 iana-time-zone-0163

define Package/nu-plugin-port-extension
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=A nushell plugin for scanning ports
  URL:=https://github.com/FMotalleb/nu_plugin_port_extension
  DEPENDS:=+nushell
  PROVIDES:=nu-plugin-port-scan
endef

define Package/nu-plugin-port-extension/description
  A nushell plugin to list all active connections and scanning ports
 on a target address.
endef

define Package/nu-plugin-port-extension/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_port_extension \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-port-extension/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_port_extension"
endef

$(eval $(call BuildPackage,nu-plugin-port-extension))
