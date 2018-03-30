# Copyright (C) 2018-2018 yayooo@gmail.com

include $(TOPDIR)/rules.mk

PKG_NAME:=baidudisk
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=cd1b4bc0f462b4a2fa2a88ab713050363d2d00af
PKG_SOURCE_URL:=https://github.com/choury/$(PKG_NAME).git

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/baidudisk
	TITLE:=baidudisk
	URL:=https://github.com/choury/$(PKG_NAME)
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Filesystem
	DEPENDS:=+kmod-fuse +libfuse +libstdcpp +libpthread +libjson-c +libopenssl +libcurl
	MAINTAINER:=yayooo@gmail.com
endef

define Package/baidudisk/description
	BaiDu PCS
endef
define Build/Configure
	cd $(PKG_BUILD_DIR) && cmake -D CMAKE_C_COMPILER="mipsel-openwrt-linux-musl-gcc" -D CMAKE_CXX_COMPILER="mipsel-openwrt-linux-musl-g++" .
endef

define Package/baidudisk/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/baidudisk $(1)/usr/bin
endef

$(eval $(call BuildPackage,baidudisk))

