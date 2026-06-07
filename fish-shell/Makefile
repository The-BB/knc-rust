# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2025-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=fish-shell
PKG_VERSION:=4.7.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/fish-shell/fish-shell/tar.gz/$(PKG_VERSION)?
PKG_HASH:=ce303c80fb61993f2ba4ceeca88e0dd6ad5876c4e064661ad31b715128dc7fe4

PKG_LICENSE:=BSD-2-Clause GPL-2.0-only GPL-2.0-or-later ISC MIT PSF-2.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Entware team, https://entware.net

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += getrandom-0217 getrandom-034

define Package/fish-shell
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Shells
  TITLE:=Friendly interactive shell
  URL:=https://fishshell.com/
  DEPENDS:=+libpcre2 +libpcre2-32
  PROVIDES:=fish
endef

define Package/fish-shell/description
 fish is a shell geared towards interactive use. Its features are
 focused on user friendliness and discoverability. The language syntax is
 simple but incompatible with other shell languages.
endef

define Package/fish-shell/conffiles
/opt/etc/fish/config.fish
endef

RUSTC_VARS += \
	PREFIX=/opt \
	BINDIR=/opt/bin \
	DATADIR=/opt/share \
	DOCDIR=/opt/share/doc \
	LOCALEDIR=/opt/share/locale \
	SYSCONFDIR=/opt/etc \
	FISH_BUILD_DOCS=0 \
	FISH_BUILD_VERSION=$(PKG_VERSION)

define Package/fish-shell/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/fish{,_indent,_key_reader} \
		$(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc/fish/{completions,conf.d,functions}
	$(CP) $(PKG_BUILD_DIR)/etc/config.fish $(1)/opt/etc/fish
	$(INSTALL_DIR) $(1)/opt/share/fish/vendor_{completions,conf,functions}.d
	$(CP) $(PKG_BUILD_DIR)/share/{completions,functions,prompts,themes} \
		 $(1)/opt/share/fish
	$(CP) $(PKG_BUILD_DIR)/share/{config,__fish_build_paths}.fish \
		 $(1)/opt/share/fish
endef

define Package/fish-shell/postinst
#!/bin/sh

grep -q 'fish' /opt/etc/shells || echo "/opt/bin/fish" >> /opt/etc/shells
endef

$(eval $(call BuildPackage,fish-shell))
