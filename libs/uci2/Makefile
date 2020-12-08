include $(TOPDIR)/rules.mk

PKG_NAME:=uci2
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/sartura/uci2.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=2d082b587d32ce019fd94317026911e9b51f90dd
PKG_MIRROR_HASH:=965339e85ff60724fc25ef812c117d203df63055821aa4d0006cc7f59c421b5b

PKG_MAINTAINER:=Jakov Petrina <jakov.petrina@sartura.hr>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libuci2/Default
	TITLE:=AST-based Unified C parser library for UCI
	URL:=https://github.com/sartura/uci2
endef

define Package/libuci2
	$(call Package/libuci2/Default)
	SECTION:=libs
	CATEGORY:=Libraries
endef

define Package/libuci2/description
UCI2 is a C library that provides an alternative UCI parser with an Abstract
Syntax Tree (AST) representation of configuration files.
endef

define Package/libuci2-example
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Example program using UCI2 runtime library
	DEPENDS:=+libuci2
endef

CMAKE_OPTIONS += \
	-DENABLE_TESTS=OFF \
	-DCMAKE_BUILD_TYPE=Release

define Build/Compile/libuci2-example
	$(MAKE) -C ./src \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -I$(PKG_BUILD_DIR)/src -L$(PKG_BUILD_DIR)" \
		LDFLAGS="$(TARGET_LDFLAGS) -L$(PKG_BUILD_DIR) -luci2" \
		DESTDIR="$(PKG_INSTALL_DIR)"
endef

define Build/Compile
	$(call Build/Compile/Default)
	$(call Build/Compile/libuci2-example)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/{libuci2,uci2_ast}.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libuci2.so $(1)/usr/lib/
endef

define Package/libuci2/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libuci2.so $(1)/usr/lib/
endef

define Package/libuci2-example/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libuci2-example $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,libuci2))
$(eval $(call BuildPackage,libuci2-example))
