#
# Copyright (C) 2016-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tftp-hpa
PKG_VERSION:=5.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://www.kernel.org/pub/software/network/tftp/tftp-hpa/
PKG_MD5SUM:=e86f58164166804e8ae5a46010f29317

include $(INCLUDE_DIR)/package.mk

define Package/tftp-hpa/Default
	SECTION:=net
	CATEGORY:=Network
	URL:=https://www.kernel.org/pub/software/network/tftp/tftp-hpa/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/tftp-hpa
	$(call Package/tftp-hpa/Default)
	TITLE:=An enhanced version of the BSD TFTP client
endef

define Package/tftpd-hpa
	$(call Package/tftp-hpa/Default)
	TITLE:=An enhanced version of the BSD TFTP server
endef

define Build/Compile	
	$(MAKE) -C $(PKG_BUILD_DIR)
endef

define Package/tftp-hpa/install	
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tftp/tftp $(1)/usr/bin/tftp
endef

define Package/tftpd-hpa/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tftpd/tftpd $(1)/usr/sbin/in.tftpd
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/tftpd-hpa.init $(1)/etc/init.d/tftpd
endef

$(eval $(call BuildPackage,tftp-hpa))
$(eval $(call BuildPackage,tftpd-hpa))

