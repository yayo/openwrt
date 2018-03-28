#
# Copyright (C) 2018-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=harfbuzz
PKG_VERSION:=1.7.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://www.freedesktop.org/software/harfbuzz/release/
PKG_HASH:=da7bed39134826cd51e57c29f1dfbe342ccedb4f4773b1c951ff05ff383e2e9b

include $(INCLUDE_DIR)/package.mk

define Package/harfbuzz
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libgcc +zlib +libbz2 +libpng +glib2 +libfreetype
	TITLE:=harfbuzz
	URL:=https://www.cairographics.org/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/harfbuzz/description
	HarfBuzz is an OpenType text shaping engine.
endef

CONFIGURE_ARGS += --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --datadir=/usr/share --sysconfdir=/etc --localstatedir=/var/lib --disable-dependency-tracking --disable-silent-rules --libdir=/usr/lib --disable-gtk-doc --disable-gtk-doc-html --disable-gtk-doc-pdf --without-coretext --without-uniscribe --disable-static --without-cairo --without-fontconfig --without-graphite2 --without-icu --disable-introspection --without-gobject --with-glib --with-freetype

define Package/harfbuzz/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/libharfbuzz.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,harfbuzz))

