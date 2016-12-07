#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sysrepo-plugin-dt-sip
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

PKG_FIXUP:=libtool
PKG_INSTALL:=1

CMAKE_OPTIONS += -DCMAKE_C_FLAGS="-Wall -g"

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/sysrepo-plugin-dt-sip
  SECTION:=net
  CATEGORY:=Network
	DEPENDS:=+libuci +libubus +sysrepoctl +sysrepo-plugind +libblobmsg-json
  TITLE:=sysrepo-plugin-dt-sip
endef

define Package/sysrepo-plugin-dt-sip/description
  sysrepo-plugin-dt-sip is a plugin daemon for sysrepo datastore. It manages SIP asterisk configuration.
endef

##new from nvram example
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
	mkdir -p $(1)/usr/lib/sysrepo/plugins
endef

define Package/sysrepo-plugin-dt-sip/install
	$(INSTALL_DIR) $(1)/usr/lib/sysrepo/plugins
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/libsysrepo-plugin-dt-sip.so $(1)/usr/lib/sysrepo/plugins

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/config/asterisk $(1)/etc/config/

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/yang/sip@2015-10-06.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/sip-plugin.default $(1)/etc/uci-defaults/sip-plugin.default
endef

$(eval $(call BuildPackage,sysrepo-plugin-dt-sip))
