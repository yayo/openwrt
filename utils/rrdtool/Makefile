#
# Copyright (C) 2018-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rrdtool
PKG_MAJOR:=1
PKG_VERSION:=$(PKG_MAJOR).7.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/rrdtool-$(PKG_VERSION)
#PKG_SOURCE_PROTO:=git
#PKG_SOURCE_VERSION:=bfc82d5242855628b826018479df00e0ec4e8360
#PKG_SOURCE_URL:=https://github.com/oetiker/$(PKG_NAME)-$(PKG_MAJOR).x.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= http://oss.oetiker.ch/rrdtool/pub/
PKG_HASH:=f97d348935b91780f2cd80399719e20c0b91f0a23537c0a85f9ff306d4c5526b

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk

define Package/rrdtool/Default
	TITLE:=Round Robin Database (RRD)
	URL:=http://oss.oetiker.ch/rrdtool/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/rrdtool/description/Default
	RRD is the Acronym for Round Robin Database. RRD is a system to store and
	display time-series data (i.e. network bandwidth, machine-room temperature,
	server load average). It stores the data in a very compact way that will
	not expand over time, and it presents useful graphs by processing the data
	to enforce a certain data density. It can be used either via simple wrapper
	scripts (from shell or Perl) or via frontends that poll network devices and
	put friendly user interface on it.
endef

define Package/librrd
$(call Package/rrdtool/Default)
	SECTION:=libs
	CATEGORY:=Libraries
	DEPENDS:=+libxml2 +cairo +pango
	TITLE+=management library
endef

define Package/librrd/description
$(call Package/rrdtool/description/Default)
	This package contains a shared library, used by other programs.
endef

define Package/rrdtool
$(call Package/rrdtool/Default)
	SECTION:=utils
	CATEGORY:=Utilities
	SUBMENU:=database
	DEPENDS:=+librrd
	TITLE+= management tools
endef

define Package/rrdtool/description
$(call Package/rrdtool/description/Default)
	This package contains command line tools used to manage RRDs.
endef

TARGET_CFLAGS += -I/usr/include/cairo

CONFIGURE_ARGS += --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --datadir=/usr/share --sysconfdir=/etc --localstatedir=/var/lib --disable-dependency-tracking --disable-silent-rules --libdir=/usr/lib --enable-rrd_graph --disable-docs --disable-lua-site-install --disable-lua --disable-perl-site-install --disable-perl --disable-python --disable-rrdcgi --disable-static --disable-tcl --without-tcllib --disable-ruby-site-install --disable-ruby --disable-libwrap --disable-libdbi --disable-librados --disable-nls

define Package/librrd/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/.libs/librrd.so* $(1)/usr/lib/
endef
define Package/rrdtool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/src/.libs/rrdtool $(1)/usr/bin/
endef

$(eval $(call BuildPackage,librrd))
$(eval $(call BuildPackage,rrdtool))

