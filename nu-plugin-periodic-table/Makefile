# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2025 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=nu-plugin-periodic-table
PKG_VERSION:=0.2.11
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/JosephTLyons/nu_plugin_periodic_table
PKG_MIRROR_HASH:=fdd9472e527bca7603db8dbec848f1eaf0875079d0383b1a68748fab9a0ab072

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=License.txt

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0440 getrandom-0215 getrandom-033 iana-time-zone-0161

define Package/nu-plugin-periodic-table
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=nu plugin a periodic table of elements
  URL:=https://github.com/JosephTLyons/nu_plugin_periodic_table
  DEPENDS:=+nushell
endef

define Package/nu-plugin-periodic-table/description
  A periodic table of elements plugin for Nushell.
endef

ifneq ($(CONFIG_ARCH_64BIT),y)
RUSTFLAGS += --cfg crossbeam_no_atomic_64
endif

define Package/nu-plugin-periodic-table/install
	$(INSTALL_DIR) $(1)/opt/usr/bin/nu_plugins
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/nu_plugin_periodic_table \
		$(1)/opt/usr/bin/nu_plugins
endef

define Package/nu-plugin-periodic-table/postinst
#!/bin/sh

nu --commands "plugin add /opt/usr/bin/nu_plugins/nu_plugin_periodic_table"
endef

$(eval $(call BuildPackage,nu-plugin-periodic-table))
