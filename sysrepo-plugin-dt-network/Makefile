#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sysrepo-plugin-dt-network
PKG_VERSION:=1.0

PKG_LICENSE:=GPL-2.0+
PKG_MAINTAINER:=Antonio Paunovic <antonio.paunovic@sartura.hr>

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/sysrepo/sysrepo-plugin-dt-network
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=81608ae88530b0ed0e3bd0673750aee18a8a97dd
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/sysrepo-plugin-dt-network
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+sysrepoctl +sysrepo-plugind +libblobmsg-json
  TITLE:=sysrepo-plugin-dt-network
endef

define Package/sysrepo-plugin-dt-network/description
  sysrepo-plugin-dt-network is a plugin daemon for sysrepo datastore. It manages network status.
endef

define Package/sysrepo-plugin-dt-network/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/sysrepo-plugin-dt-network.so $(1)/usr/lib/sysrepo/plugins

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/yang/ietf-ip@2014-06-16.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/yang/ietf-interfaces@2014-05-08.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/network-plugin.default $(1)/etc/uci-defaults/network-plugin.default
endef

$(eval $(call BuildPackage,sysrepo-plugin-dt-network))
