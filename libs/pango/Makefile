#
# Copyright (C) 2018-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pango
VER_MAJOR:=1.40
PKG_VERSION:=${VER_MAJOR}.14
PKG_RELEASE:=1

# grep 'fontconfig >=' pango-1.41.1/configure.ac 
#  PKG_CHECK_MODULES(FONTCONFIG, fontconfig >= 2.11.91, have_fontconfig=true, :)
# 
# grep ^Version: /usr/lib/pkgconfig/fontconfig.pc
#  Version: 2.11.1
#

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.gnome.org/pub/gnome/sources/pango/${VER_MAJOR}/
PKG_HASH:=90af1beaa7bf9e4c52db29ec251ec4fd0a8f2cc185d521ad1f88d01b3a6a17e3

include $(INCLUDE_DIR)/package.mk

LIBPANGO_DEPENDS:= +libgcc +libffi +glib2
LIBPANGOFT2_DEPENDS:= ${LIBPANGO_DEPENDS} +libexpat +fontconfig +harfbuzz
LIBPANGOCAIRO_DEPENDS:= ${LIBPANGOFT2_DEPENDS} +cairo

define Package/pango
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=${LIBPANGOCAIRO_DEPENDS}
	TITLE:=pango
	URL:=https://www.cairographics.org/
	MAINTAINER:=yayooo@gmail.com
endef
define Package/pango/description
	Pango is a library for laying out and rendering of text, with an emphasis on internationalization.
endef

CONFIGURE_ARGS += --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --datadir=/usr/share --sysconfdir=/etc --localstatedir=/var/lib --disable-dependency-tracking --disable-silent-rules --libdir=/usr/lib --disable-gtk-doc --disable-gtk-doc-html --disable-gtk-doc-pdf --disable-introspection --without-xft --with-cairo 

define Package/pango/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpango-1.0.so* $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpangoft2-1.0.so* $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpangocairo-1.0.so* $(1)/usr/lib
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/pango
	$(CP) $(PKG_BUILD_DIR)/pango/pango{,-version-macros,-types,-enum-types,-attributes,-features,-tabs,-engine,-item,-utils,-bidi-type,-break,-context,-coverage,-font,-fontmap,-fontset,-glyph,-glyph-item,-gravity,-language,-layout,-matrix,-renderer,-script,cairo}.h $(1)/usr/include/pango
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpango-1.0.so* $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpangoft2-1.0.so* $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/pango/.libs/libpangocairo-1.0.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,pango))

