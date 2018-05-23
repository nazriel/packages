#
# Copyright (C) 2012-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libimobiledevice
PKG_RELEASE:=2

PKG_MAINTAINER:=Lukasz Baj <l.baj@radytek.com>
PKG_LICENSE:=LGPL-2.1+
PKG_LICENSE_FILES:=COPYING.LESSER

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2018-04-27
PKG_SOURCE_URL:=https://github.com/libimobiledevice/libimobiledevice.git
PKG_SOURCE_VERSION:=26373b334889f5ae2e2737ff447eb25b1700fa2f
PKG_MIRROR_HASH:=11fe19d597a0edebe6828126695dde044ae7a2218ca014ffd614e118cd8779aa

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk
include ../../lang/python/python-package.mk

define Package/libimobiledevice/Default
  TITLE:=A library that talks to Apple devices.
  URL:=http://www.libimobiledevice.org/
endef

define Package/libimobiledevice/Default/description
  libimobiledevice is a software library that talks the protocols to support
  iPhone®, iPod Touch®, iPad® and Apple TV® devices.
endef

define Package/libimobiledevice
  $(call Package/libimobiledevice/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=$(ICONV_DEPENDS) +libplist +libusbmuxd +libopenssl
endef

define Package/libimobiledevice/description
  $(call Package/libimobiledevice/Default/description)
endef

define Package/libimobiledevice-utils
  $(call Package/libimobiledevice/Default)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libimobiledevice
endef

define Package/libimobiledevice-utils/description
  $(call Package/libimobiledevice/Default/description)
  This package contains the libimobiledevice utilities.
endef

CONFIGURE_VARS += \
	libusbmuxd_CFLAGS="-I$(STAGING_DIR)/usr/include" \
	libusbmuxd_LIBS="-L$(STAGING_DIR)/usr/lib -lusbmuxd" \
	openssl_CFLAGS=" " \
	openssl_LIBS="-L$(STAGING_DIR)/usr/lib -lssl -lcrypto"

CONFIGURE_ARGS += \
	--without-cython \
	--disable-largefile

TARGET_LDFLAGS += -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libimobiledevice $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libimobiledevice.{a,la,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libimobiledevice-*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libimobiledevice/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libimobiledevice.so.* $(1)/usr/lib/
endef

define Package/libimobiledevice-utils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/idevice* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,libimobiledevice))
$(eval $(call BuildPackage,libimobiledevice-utils))
