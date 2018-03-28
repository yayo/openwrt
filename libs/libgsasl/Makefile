#
# Copyright (C) 2018-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libgsasl
PKG_VERSION:=1.8.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
#PKG_SOURCE_PROTO:=git
#PKG_SOURCE_VERSION:=524db10028ee3c2ea6f7f89ecf0be087b0dc7c2e
#PKG_SOURCE_URL:=https://git.savannah.gnu.org/git/$(PKG_NAME).git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://ftp.gnu.org/gnu/$(PKG_NAME)/
PKG_HASH:=3adfb49f9c92a719dea855fd1840d698cde55d4648d332a69032ba8bea207720

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/libgsasl
  TITLE:=libgsasl
  URL:=https://www.gnu.org/software/gsasl/
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libgcc
  MAINTAINER:=yayooo@gmail.com
endef

define Package/libgsasl/description
	GNU SASL is an implementation of the Simple Authentication and Security Layer framework and a few common SASL mechanisms.
endef

CONFIGURE_ARGS += --disable-nls --disable-obsolete

define Package/libgsasl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libgsasl.so* $(1)/usr/lib
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/src/gsasl{,-mech,-compat}.h $(1)/usr/include
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libgsasl.so* $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_BUILD_DIR)/libgsasl.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,libgsasl))

