#
# Copyright (C) 2016-2018 yayooo@gmail.com
#

include $(TOPDIR)/rules.mk

PKG_NAME:=opensmtpd
PKG_VERSION:=6.0.3p1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.opensmtpd.org/archives/
PKG_HASH:=291881862888655565e8bbe3cfb743310f5dc0edb6fd28a889a9a547ad767a81

include $(INCLUDE_DIR)/package.mk

define Package/opensmtpd
	SECTION:=mail
	CATEGORY:=Mail
	DEPENDS:=+libgcc +musl-fts +libasr +libevent2 +zlib +libopenssl
	TITLE:=OpenSMTPD is a FREE implementation of the server-side SMTP protocol as defined by RFC 5321
	URL:=https://www.opensmtpd.org/
	USERID:=smtpd=25:smtpd=25
	MAINTAINER:=yayooo@gmail.com
endef

define Package/opensmtpd/description
	OpenSMTPD is a FREE implementation of the SMTP protocol with some common
	extensions. It allows ordinary machines to exchange e-mails with systems
	speaking the SMTP protocol. It implements a fairly large part of RFC5321
	and can already cover a large range of use-cases.
endef

CONFIGURE_ARGS += --without-table-db --with-user-smtpd=smtpd --with-user-queue=smtpd --with-group-queue=smtpd --with-path-socket=/var/run --sysconfdir=/etc/smtpd --without-auth-pam --with-path-CAfile=/etc/ssl/certs/ca-certificates.crt

SMTPD_CONF:=/etc/smtpd/smtpd.conf

define Package/opensmtpd/install
	$(INSTALL_DIR) $(1)/etc/smtpd
	echo -e "# http://man.openbsd.org/smtpd.conf \nmax-message-size 67108863\nlisten on socket\n#listen on 127.0.0.1 inet4 port 25\ntable t1 {u1=YOU_NAME@YOUR_DOMAIN.net:YOUR_PASSWORD}\naccept from any sender "YOU_NAME@YOUR_DOMAIN.net" for any relay via smtps+auth://u1@smtp.YOUR_SERVER.net:465 auth <t1> as YOU_NAME@YOUR_DOMAIN.net" > $(1)${SMTPD_CONF}
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mk/smtpd/smtpd $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mk/smtpctl/smtpctl $(1)/usr/sbin/
	ln $(1)/usr/sbin/smtpctl $(1)/usr/sbin/sendmail
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) src/openwrt/init.d/smtpd $(1)/etc/init.d/smtpd
endef

define Package/opensmtpd/conffiles
	${SMTPD_CONF}
endef

define Package/opensmtpd/postinst
	mkdir -p --mode=711 /var/spool/smtpd
endef

define Package/opensmtpd/postrm
	rm -rf $${IPKG_INSTROOT}/var/spool/smtpd
	rmdir -p --ignore-fail-on-non-empty $${IPKG_INSTROOT}/var/spool
	rmdir -p --ignore-fail-on-non-empty $${IPKG_INSTROOT}/etc/smtpd
endef

$(eval $(call BuildPackage,opensmtpd))

