include $(TOPDIR)/rules.mk

PKG_NAME:=opera-proxy
PKG_VERSION:=1.1.0          # если у вас другая версия, укажите её
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/oskord-sudo/opera-proxy.git
PKG_SOURCE_VERSION:=HEAD
PKG_MIRROR_HASH:=skip

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/opera-proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Opera VPN/Proxy service
  URL:=https://github.com/oskord-sudo/opera-proxy
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/opera-proxy/description
  A tool that uses Opera VPN/proxy infrastructure.
  Built via GitHub Actions for OpenWrt 25.12.0 (x86_64).
endef

GO_PKG:=github.com/oskord-sudo/opera-proxy
GO_PKG_LDFLAGS:=-X main.version=$(PKG_VERSION)

define Package/opera-proxy/install
  $(INSTALL_DIR) $(1)/usr/bin
  $(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/opera-proxy $(1)/usr/bin/
endef

$(eval $(call GoPackage,opera-proxy))
