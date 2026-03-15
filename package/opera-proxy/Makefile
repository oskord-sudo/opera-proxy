include $(TOPDIR)/rules.mk

PKG_NAME:=opera-proxy
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/opera-proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Opera VPN/Proxy service (test)
endef

define Build/Compile
endef

define Package/opera-proxy/install
	$(INSTALL_DIR) $(1)/usr/bin
	echo "#!/bin/sh" > $(1)/usr/bin/opera-proxy
	echo "echo test" >> $(1)/usr/bin/opera-proxy
	chmod +x $(1)/usr/bin/opera-proxy
endef

$(eval $(call BuildPackage,opera-proxy))
