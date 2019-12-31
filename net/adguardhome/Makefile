#
# Copyright (C) 2019 IMXQD
#
# IMXQD <ahtlxqd@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=AdGuardHome
PROJECT_NAME:=AdGuardHome
PKG_VERSION:=0.100.8
PKG_RELEASE:=1

PKG_SOURCE:=AdGuardHome-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/AdguardTeam/AdGuardHome/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/AdGuardHome-$(PKG_VERSION)

PKG_BUILD_DEPENDS:=golang/host node/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
STRIP:=true
GO_PKG:=github.com/AdguardTeam/AdGuardHome
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:=main.version=v$(PKG_VERSION)
GO_PKG_GCFLAGS:="-trimpath=$(PWD)"

include $(INCLUDE_DIR)/package.mk
include ../../lang/golang/golang-package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Network-wide ads & trackers blocking DNS server
	URL:=https://github.com/AdguardTeam/AdGuardHome
	DEPENDS:=$(GO_ARCH_DEPENDS)
endef


define Package/$(PKG_NAME)/description
Network-wide ads & trackers blocking DNS server
endef

define Build/Configure
	( \
		cd $(PKG_BUILD_DIR); \
		npm --prefix client ci; \
		npm --prefix client run build-prod; \
		export GOPATH=$(GO_PKG_TMP_DIR) ; \
		GO111MODULE=off go get -v github.com/gobuffalo/packr/... ; \
		$(GO_PKG_TMP_DIR)/bin/packr clean ; \
		$(GO_PKG_TMP_DIR)/bin/packr -i ./home -zv ; \
		unset GOPATH \
	)
	$(call GoPackage/Build/Configure)
endef

Build/Compile=$(call GoPackage/Build/Compile)

define Package/$(PKG_NAME)/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))
	$(INSTALL_DIR) $(1)/usr/bin/AdGuardHome
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/AdGuardHome $(1)/usr/bin/AdGuardHome/$(PKG_NAME)
endef

$(eval $(call GoBinPackage,AdGuardHome))
$(eval $(call BuildPackage,AdGuardHome))