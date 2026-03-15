include $(TOPDIR)/rules.mk

PKG_NAME:=opera-proxy
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_PROTO:=none
PKG_MIRROR_HASH:=skip

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/opera-proxy
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Opera VPN/Proxy service
  URL:=https://github.com/oskord-sudo/opera-proxy
  DEPENDS:=+ca-bundle
endef

define Build/Compile
	# Отладка: показываем, где мы находимся и что есть
	echo "=== PKG_BUILD_DIR ==="
	echo $(PKG_BUILD_DIR)
	cd $(PKG_BUILD_DIR) && \
	echo "=== Содержимое директории сборки (первые 30 элементов) ===" && \
	ls -la && \
	echo "=== Поиск всех .go файлов (первые 20) ===" && \
	find . -name "*.go" -type f | head -20 && \
	echo "=== Попытка найти main.go ===" && \
	find . -name "main.go" -type f || echo "main.go не найден" && \
	echo "=== Запуск go build ===" && \
	export GO111MODULE=on && \
	export GOPROXY=https://proxy.golang.org && \
	export GOOS=linux && \
	export GOARCH=amd64 && \
	# Если main.go в корне, то go build .; если в подпапке, укажем её, например ./cmd/opera-proxy
	# Пробуем разные варианты:
	if [ -f "main.go" ]; then \
		go build -o opera-proxy .; \
	elif [ -f "cmd/opera-proxy/main.go" ]; then \
		cd cmd/opera-proxy && go build -o ../../opera-proxy .; \
	elif [ -f "src/main.go" ]; then \
		cd src && go build -o ../opera-proxy .; \
	else \
		echo "Не удалось найти main.go, пробуем сборку текущей директории..."; \
		go build -o opera-proxy .; \
	fi
endef

define Package/opera-proxy/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/opera-proxy $(1)/usr/bin/
endef

$(eval $(call BuildPackage,opera-proxy))
