#
# Copyright (C) 2016-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libasr
PKG_VERSION:=201602131606
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.opensmtpd.org/archives/
PKG_HASH:=e5684a08d5eb61d68a94a24688f23bee8785c8a51a1bd34c88cae5aee5aa6da2

include $(INCLUDE_DIR)/package.mk

define Package/libasr
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=ASynchronous Resolver library
	URL:=https://github.com/OpenSMTPD/libasr
	MAINTAINER:=yayooo@gmail.com
endef

define Package/libasr/description
  libasr is a free, simple and portable asynchronous resolver library.
endef


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/src/asr.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libasr.so* $(1)/usr/lib/
endef

define Package/libasr/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libasr.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libasr))

