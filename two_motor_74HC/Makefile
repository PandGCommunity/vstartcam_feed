include $(TOPDIR)/rules.mk
#Based on adb package from AUR https://aur.archlinux.org/packages/adb/ , reused Makefile

PKG_NAME:=two_motor_74HC
PKG_VERSION:=0.0.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://android.googlesource.com/platform/system/core
PKG_SOURCE_VERSION:=6fe92d1a3fb17545d82d020a3c995f32e6b71f9d
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_MAINTAINER:=Henryk Heisig <hyniu@o2.pl>


https://github.com/PandGCommunity/two_motor_74HC.git
#
# Copyright (C) 2011-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=two_motor_74HC
PKG_VERSION:=0.0.3
PKG_MAINTAINER:=Sergey Sharshunov <s.sharshunov@gmail.com>

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/PandGCommunity/two_motor_74HC.git
PKG_SOURCE_VERSION:=39987411f913ca905773f7f1a48054486a677487

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)
# PKG_BUILD_DEPENDS:=hisi-osdrv2

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
	SECTION:=pandgc
	CATEGORY:=PandGCommunity
	SUBMENU:=Utils
	TITLE:=VSTARTCAM MOTOR DRIVER
	MAINTAINER:=s.sharshunov@gmail.com
	DEPENDS:=@(TARGET_ramips_rt305x_DEVICE_rt5350f-t7838wip)
endef

define Package/$(PKG_NAME)/description
	Vstartcam motor driver
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
