#
# Copyright (C) 2016-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=p7zip
PKG_VERSION:=16.02
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_src_all.tar.bz2
PKG_SOURCE_URL:=https://downloads.sourceforge.net/project/p7zip/p7zip/$(PKG_VERSION)/
PKG_MD5SUM:=a0128d661cfe7cc8c121e73519c54fbf

include $(INCLUDE_DIR)/package.mk

define Package/p7zip
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=Compression
	DEPENDS:=+libgcc +libstdcpp
	TITLE:=Archiver for .7z files
	URL:=http://www.7-zip.org/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/p7zip/description
	p7zip is a port of 7za.exe for POSIX systems like Unix
endef

UNPACK_CMD=bzip2 -dc $(DL_DIR)/$(PKG_SOURCE) | tar -C $(PKG_BUILD_DIR) -xf -
define Build/Prepare
	$(PKG_UNPACK)
	$(CP) src/makefile.mipsel-openwrt-linux-musl $(PKG_BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)/makefile.machine
	$(Build/Patch)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION) -f makefile 7z
endef

define Package/p7zip/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)/bin/7z $(1)/usr/bin/7z
	$(INSTALL_DIR) $(1)/usr/lib/p7zip
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)/bin/7z.so $(1)/usr/lib/p7zip/7z.so
	$(INSTALL_DIR) $(1)/usr/lib/p7zip/Codecs
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)/bin/Codecs/Rar.so $(1)/usr/lib/p7zip/Codecs/Rar.so
endef

define Package/p7zip/postrm
	rm -rf $${IPKG_INSTROOT}/usr/lib/p7zip
endef

$(eval $(call BuildPackage,p7zip))
