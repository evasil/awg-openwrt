# SPDX-License-Identifier: GPL-3.0-or-later
include $(TOPDIR)/rules.mk

PKG_NAME:=opendht
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

# Источники
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/savoirfairelinux/opendht.git
PKG_SOURCE_VERSION:=master
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/opendht
  SECTION:=net
  CATEGORY:=Network
  TITLE:=OpenDHT - statically linked DHT node
endef

define Package/opendht/description
  OpenDHT statically compiled DHT node for OpenWRT
endef

# Подготовка
define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)/build
endef

# Конфигурация CMake для статической сборки
define Build/Configure
	cd $(PKG_BUILD_DIR)/build && \
	cmake .. \
	  -DCMAKE_TOOLCHAIN_FILE=$(STAGING_DIR)/toolchain.cmake \
	  -DBUILD_SHARED_LIBS=OFF \
	  -DCMAKE_POSITION_INDEPENDENT_CODE=ON
endef

# Компиляция
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/build -j$(HOST_JOBS)
endef

# Установка
define Package/opendht/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/dhtnode $(1)/usr/bin/
endef

$(eval $(call BuildPackage,opendht))
