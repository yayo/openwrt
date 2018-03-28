include $(TOPDIR)/rules.mk
PKG_NAME := HelloWorld
PKG_RELEASE := 1
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)
include $(INCLUDE_DIR)/package.mk
define Package/helloworld
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=HelloWorld
	DEPENDS:=+libc +libgcc
	MAINTAINER:=yayooo@gmail.com
endef
# echo libc.so > staging_dir/target-mipsel_24kec+dsp_musl-1.1.15/pkginfo/libc.provides
# echo libgcc_s.so.1 > staging_dir/target-mipsel_24kec+dsp_musl-1.1.15/pkginfo/libgcc.provides
define Package/helloworld/description
	Say Hello to the World !
endef
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef
define Package/helloworld/install
	$(INSTALL_DIR) $(1)/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/helloworld $(1)/bin/
endef
$(eval $(call BuildPackage,helloworld))
