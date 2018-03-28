# Copyright (C) 2018-2018 yayooo@gmail.com

include $(TOPDIR)/rules.mk

PKG_NAME:=exfat
PKG_VERSION:=1.2.8
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=0d19b6418ecbd7e1807dadc79a37785c9443f431
PKG_SOURCE_URL:=https://github.com/relan/$(PKG_NAME).git

PKG_FIXUP:=autoreconf
PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/exfat
  TITLE:=exfat
  URL:=https://github.com/relan/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  DEPENDS:=+kmod-fuse +libfuse +libpthread
  MAINTAINER:=yayooo@gmail.com
endef

define Package/exfat/description
 Full-featured exFAT file system implementation for Unix-like systems.
 It consists of a FUSE module (fuse-exfat) and a set of utilities (exfat-utils).
endef

define Package/exfat/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fuse/mount.exfat-fuse $(1)/sbin/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mkfs/mkexfatfs $(1)/usr/bin/mkfs.exfat
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fsck/exfatfsck $(1)/usr/bin/fsck.exfat
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/label/exfatlabel $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dump/dumpexfat $(1)/usr/bin/
endef

define Package/exfat/postinst
#!/bin/sh
 if [ -z "$${IPKG_INSTROOT}" ] ; then
  LINK=/sbin/mount.exfat
   [ -e $${LINK} ] || ln -sr $${LINK}-fuse $${LINK}
 fi
 exit 0
endef

define Package/exfat/prerm
#!/bin/sh
 if [ -z "$${IPKG_INSTROOT}" ] ; then
  LINK=/sbin/mount.exfat
   [ -h $${LINK} ] && [ "$${LINK}-fuse" == "$$(readlink -f $${LINK})" ] && rm -f $${LINK}
 fi
 exit 0
endef

$(eval $(call BuildPackage,exfat))

