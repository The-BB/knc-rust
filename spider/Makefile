# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024-2026 Entware

include $(TOPDIR)/rules.mk

PKG_NAME:=spider
PKG_VERSION:=2.48.13
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/spider-rs/spider/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=75bd5efbb52868a7b9ad456c45638722660c52fea93df5ff40c129f997111faa

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Entware team, https://entware.net

include $(INCLUDE_DIR)/package.mk
include ../rustc-dev/cargo.mk

PKG_BUILD_DEPENDS += \
	chromey-24212 chrono-0444 getrandom-0217 getrandom-034 getrandom-042 \
	iana-time-zone-0164 rmcp-120

define Package/spider/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=https://github.com/spider-rs/spider
  DEPENDS:=+libopenssl @!USE_MUSL
endef

define Package/spider-cli
  $(call Package/spider/Default)
  TITLE:=The fastest web crawler CLI
endef

define Package/spider-mcp
  $(call Package/spider/Default)
  TITLE:=MCP (Model Context Protocol) server
endef

define Package/spider-worker
  $(call Package/spider/Default)
  TITLE:=The fastest web crawler as a worker or proxy
endef

define Package/spider/description
  The fastest web crawler and indexer.
endef

define Package/spider-cli/description
  $(call Package/spider/description)
  A fast command line spider or crawler.
endef

define Package/spider-mcp/description
  $(call Package/spider/description)
  MCP (Model Context Protocol) server exposing Spider web crawler capabilities
  as tools.
endef

define Package/spider-worker/description
  $(call Package/spider/description)
  A spider worker to decentralize the crawl lifting.
endef

# IO_URING since Linux 5.1
CARGO_ARGS += --no-default-features --features=basic

define Package/spider-cli/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/spider $(1)/opt/usr/bin
endef

define Package/spider-mcp/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/spider-mcp $(1)/opt/usr/bin
endef

define Package/spider-worker/install
	$(INSTALL_DIR) $(1)/opt/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/spider_worker $(1)/opt/usr/bin
endef

$(eval $(call BuildPackage,spider-cli))
$(eval $(call BuildPackage,spider-mcp))
$(eval $(call BuildPackage,spider-worker))
