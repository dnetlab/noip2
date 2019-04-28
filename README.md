# noip2
a copy from http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz

## Makefile For Openwrt
```Makefile
#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=noip2
PKG_VERSION:=2.1.9
PKG_RELEASE:=$(PKG_SOURCE_VERSION)

PKG_LICENSE:=GPL-2.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/dnetlab/noip2.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=f729d60aae5c5283f856bed5f413688e0c946abb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Dnetlab
  SUBMENU:=ddns
  TITLE:=a second-generation Linux client for the no-ip.com dynamic DNS service
  URL:=http://www.ez-ip.net
  DEPENDS:=+ddns
endef

define Package/$(PKG_NAME)/description
 No-IP offers DNS services, email, network monitoring and SSL certificates. 
 Email services include POP3 email, outbound SMTP email, backup mail services 
 and mail reflection and filtering.
endef

define Build/Compile/$(PKG_NAME)
	$(MAKE) -C $(PKG_BUILD_DIR)/noip2 \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		CPPFLAGS="$(TARGET_CPPFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/noip2 $(1)/usr/sbin/
endef
# $(INSTALL_BIN) $(PKG_BUILD_DIR)/ez-ipupdate/ez-ipupdate $(1)/usr/sbin/

$(eval $(call BuildPackage,$(PKG_NAME)))
```