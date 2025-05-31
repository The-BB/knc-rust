# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-file
PKG_VERSION:=0.15.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/fdncred/nu_plugin_file
PKG_MIRROR_HASH:=8433594650d3fd5427ced728fa406f0174e260686d7b135a8aee98fb50f9e651

PKG_LICENSE:=AGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0215 iana-time-zone-0161 specta-105

define Package/nu-plugin-file
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=a nushell plugin called file
  URL:=https://github.com/fdncred/nu_plugin_file
  DEPENDS:=+nushell
endef

define Package/nu-plugin-file/description
  A nushell plugin that will inspect a file and return information
  based on it's magic number.
endef

define Package/nu-plugin-file/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_file \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-file/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_file"
endef

$(eval $(call BuildPackage,nu-plugin-file))
