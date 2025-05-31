# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-parquet
PKG_VERSION:=0.14.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/fdncred/nu_plugin_parquet
PKG_MIRROR_HASH:=f51fc77dc547b5ac5b92be8850896137eeebf545b057836254267d49c2bcc4ec

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0215 iana-time-zone-0161

define Package/nu-plugin-parquet
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=nu plugin to add parquet support
  URL:=https://github.com/jakeswenson/nu_plugin_parquet
  DEPENDS:=+nushell
  PROVIDES:=nu-plugin-from-parquet
endef

define Package/nu-plugin-parquet/description
  This is a nushell plugin to parse parquet data files into nu
  structured types.
endef

define Package/nu-plugin-parquet/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_parquet \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-parquet/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_parquet"
endef

$(eval $(call BuildPackage,nu-plugin-parquet))
