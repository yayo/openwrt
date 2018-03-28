#
# Copyright (C) 2018-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cairo
PKG_VERSION:=1.14.12
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://cairographics.org/releases/
PKG_HASH:=8c90f00c500b2299c0a323dd9beead2a00353752b2092ead558139bd67f7bf16

include $(INCLUDE_DIR)/package.mk

define Package/cairo
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libgcc +zlib +libbz2 +libpng +libexpat +pixman +libfreetype +fontconfig 
	TITLE:=cairo
	URL:=https://www.cairographics.org/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/cairo/description
	A vector graphics library with cross-device output support
endef

PKG_FIXUP:=autoreconf

CONFIGURE_ARGS += --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --datadir=/usr/share --sysconfdir=/etc --localstatedir=/var/lib --disable-dependency-tracking --disable-silent-rules --docdir=/usr/share/doc/cairo --htmldir=/usr/share/doc/cairo/html --libdir=/usr/lib --disable-dependency-tracking --disable-gtk-doc --disable-gtk-doc-html --disable-gtk-doc-pdf --without-x --disable-tee --disable-xlib --disable-xlib-xrender --disable-quartz --disable-quartz-image --disable-test-surfaces --disable-glesv2 --disable-gobject --disable-gl --disable-static --disable-valgrind --disable-xcb --disable-xcb-shm --disable-pdf --disable-ps --disable-drm --disable-directfb --disable-gallium --disable-qt --disable-vg --disable-xlib-xcb --disable-xml --enable-png --enable-ft --enable-fc --enable-svg=yes 
define Package/cairo/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libcairo.so* $(1)/usr/lib/
endef

define Build/InstallDev          
	$(INSTALL_DIR) $(1)/usr/include/cairo
	$(CP) $(PKG_BUILD_DIR)/src/cairo{,-version,-features,-ft,-svg,-deprecated}.h $(1)/usr/include/cairo
	$(INSTALL_DIR) $(1)/usr/lib                                
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libcairo.so* $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_BUILD_DIR)/src/cairo{,-ft}.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,cairo))

