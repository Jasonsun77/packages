#
# Copyright (C) 2019 IMXQD <ahtlxqd@gmail.com>
#
# This is free software, licensed under the MIT.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=minisign
PKG_VERSION:=0.8
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/jedisct1/minisign/tar.gz/$(PKG_VERSION)?
PKG_HASH:=130eb5246076bc7ec42f13495a601382e566bb6733430d40a68de5e43a7f1082

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=IMXQD <ahtlxqd@gmail.com>

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/minisign
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Minisign is a dead simple tool to sign files and verify signatures.
	DEPENDS:=+libsodium
	URL:=https://github.com/jedisct1/minisign
	SUBMENU:=Terminal
endef

define Package/minisign/description
Minisign is a dead simple tool to sign files and verify signatures.
endef

define Package/minisign/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/minisign $(1)/usr/bin/
endef

$(eval $(call BuildPackage,minisign))
