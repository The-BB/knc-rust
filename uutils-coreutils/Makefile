# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=coreutils
PKG_VERSION:=0.8.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/uutils/coreutils/tar.gz/$(PKG_VERSION)?
PKG_HASH:=03f765fd23e9cc66f8789edc6928644d8eae5e5a7962d83795739d0a8a85eaef

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += chrono-0443 getrandom-0217 getrandom-042 iana-time-zone-0164

# XXX without:  chcon & runcon (depends on SELinux);
#		stdbuf (fail to compile on several platforms).

COREUTILS_APPS:= \
	arch \
	base32 base64 basename basenc \
	cat chgrp chmod chown chroot cksum comm cp csplit cut \
	date dd df dir dircolors dirname du \
	echo env expand expr \
	factor false fmt fold \
	groups \
	head hostid hostname \
	id install \
	join \
	kill \
	link ln logname ls \
	mkdir mkfifo mknod mktemp more mv \
	nice nl nohup nproc numfmt \
	od \
	paste pathchk pr printenv printf ptx pwd \
	readlink realpath rm rmdir \
	seq shred shuf sleep sort split stat stty sum sync \
	tac tail tee test timeout touch tr true truncate tsort tty \
	uname unexpand uniq unlink \
	vdir \
	wc whoami \
	yes

DEPENDS_pinky = @!USE_MUSL
DEPENDS_uptime = @!USE_MUSL
DEPENDS_users = @!USE_MUSL
DEPENDS_who = @!USE_MUSL

# error[E0432]: unresolved imports `uucore::utmpx`, `uucore::utmpx`
ifneq ($(CONFIG_USE_MUSL),y)
COREUTILS_APPS += pinky uptime users who
endif

define Package/uutils-coreutils/Default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=The GNU coreutils, written in Rust
  URL:=https://github.com/uutils/coreutils
endef

define Package/uutils-coreutils-apps
  $(call Package/uutils-coreutils/Default)
  TITLE+=(multicall)
  VARIANT:=apps
endef

define Package/uutils-coreutils-full
  $(call Package/uutils-coreutils/Default)
  MENU:=1
  VARIANT:=full
endef

define GenBins
 define Package/$(1)
  $$(call Package/uutils-coreutils/Default)
   DEPENDS:=uutils-coreutils-full $(DEPENDS_$(2))
   TITLE:=Utility $(2) from the Rust coreutils
 endef

 define Package/$(1)/description
  $(2)
  uutils coreutils is a cross-platform reimplementation of the GNU coreutils
  in Rust. While all programs have been implemented, some options might be
  missing or different behavior might be experienced.
 endef
endef

$(foreach b,$(COREUTILS_APPS),$(eval $(call GenBins,uutils-coreutils-$(b),$(b))))

define Package/uutils-coreutils-apps/description
  A multicall (BusyBox-type) binary.
  uutils coreutils is a cross-platform reimplementation of the GNU coreutils
  in Rust. While all programs have been implemented, some options might be
  missing or different behavior might be experienced.
endef

RUSTC_VARS += PROJECT_NAME_FOR_VERSION_STRING="uutils coreutils"

ifeq ($(CONFIG_x86_64),y)
RUSTFLAGS += -C relocation-model=pic
endif

ifeq ($(BUILD_VARIANT),apps)
  CARGO_ARGS += --features="$(COREUTILS_APPS)"
endif

ifeq ($(BUILD_VARIANT),apps)
  define Package/uutils-coreutils-apps/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/coreutils $(1)/opt/usr/bin

	for apps in $(COREUTILS_APPS); do \
		$(LN) coreutils $(1)/opt/usr/bin/uu_$$$$apps ; \
	done
  endef
else
  define Build/Compile/Cargo
	for bins in $(COREUTILS_APPS); do \
		cd $(CARGO_SOURCE_DIR) && \
		$(RUSTC_VARS) RUSTFLAGS="$(RUSTFLAGS)" \
		cargo build $(CARGO_ARGS) \
		--profile $(CARGO_PKG_PROFILE) \
		--manifest-path $(CARGO_SOURCE_DIR)/Cargo.toml \
		--artifact-dir $(CARGO_INSTALL_ROOT)/bin \
		$(if $(findstring s,$(OPENWRT_VERBOSE)),--verbose) \
		-p uu_$$$$bins; \
	done
  endef

  define Package/uutils-coreutils-full/install
	true
  endef

  define InstallBins
    define Package/$(1)/install
	$(INSTALL_DIR) $$(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/$(2) $$(1)/opt/usr/bin/$(2)
    endef

    $$(eval $$(call BuildPackage,$(1)))
  endef
endif

$(eval $(call BuildPackage,uutils-coreutils-full))
$(foreach b,$(COREUTILS_APPS),$(eval $(call InstallBins,uutils-coreutils-$(b),$(b))))

$(eval $(call BuildPackage,uutils-coreutils-apps))
