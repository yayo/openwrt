#
# Copyright (C) 2016-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mailutils
PKG_VERSION:=3.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://ftp.gnu.org/gnu/mailutils/
PKG_HASH:=f39f528cf6eebc9a045658bd98c86619002f06df4664647e4f78e27e90c62173

include $(INCLUDE_DIR)/package.mk

define Package/mailutils
	SECTION:=mail
	CATEGORY:=Mail
	DEPENDS:=+libgcc +libgsasl +libgnutls
	TITLE:=GNU Mailutils
	URL:=http://mailutils.org/
	MAINTAINER:=yayooo@gmail.com
endef

define Package/mailutils/description
	Mailer(MUA) & SMTP(MTA)
endef

CONFIGURE_ARGS += --disable-nls --disable-pam --disable-virtual-domains --disable-imap --disable-pop --disable-nntp --disable-mh --disable-maildir --disable-prog --disable-radius --disable-python --disable-build-pop3d --disable-build-imap4d --disable-build-comsat --disable-build-frm --disable-build-maidag --disable-build-sieve --disable-build-messages --disable-build-readmsg --disable-build-dotlock --disable-build-movemail --disable-build-mimeview --disable-build-mh --without-readline --without-fribidi --disable-ipv6 --with-gsasl --with-gnutls --enable-smtp

define Build/Configure
	(cd $(PKG_BUILD_DIR) && aclocal && autoreconf)
	$(call Build/Configure/Default)
endef

define Package/mailutils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mail/.libs/mail $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/lib/.libs/libmuaux.so.* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libmailutils/.libs/libmailutils.so.* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libproto/mbox/.libs/libmu_mbox.so.* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libproto/mailer/.libs/libmu_mailer.so.* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/libmu_auth/.libs/libmu_auth.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,mailutils))

