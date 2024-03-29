#
# Copyright (C) 2006-2018 OpenWrt.org
# Copyright (C) 2016 Cesnet, z.s.p.o.
# Copyright (C) 2017 - 2018 Jiri Slachta <jiri@slachta.eu>
# Copyright (C) 2023 Sergey Sharshunov <s.sharshunov@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pjproject
PKG_VERSION:=2.7.2
PKG_RELEASE:=2

PKG_SOURCE:=pjproject-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.pjsip.org/release/$(PKG_VERSION)
PKG_HASH:=9c2c828abab7626edf18e04b041ef274bfaa86f99adf2c25ff56f1509e813772
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=Sergey Sharshunov <s.sharshunov@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_CONFIG_DEPENDS:=CONFIG_SOFT_FLOAT

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/pjproject/Default
  SECTION:=pandgc
  CATEGORY:=PandGCommunity
  SUBMENU:=Telephony
  URL:=http://www.pjsip.org
  DEPENDS:=$(CXX_DEPENDS) +libopenssl +libuuid +libpthread +AUDIO_SUPPORT:alsa-lib
endef

define Package/pjproject/install/lib
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/$(2).so* $(1)/usr/lib
endef

define PJSIPpackage
  define Package/$(1)
  $$(call Package/pjproject/Default)
    TITLE:=$(1) library
    DEPENDS+=$(3)
  endef

  define Package/$(1)/install
$(call Package/pjproject/install/lib,$$(1),$2)
  endef

  $$(eval $$(call BuildPackage,$(1)))
endef

CONFIGURE_ARGS+= \
	$(if $(CONFIG_SOFT_FLOAT),--disable-floating-point) \
	--with-ssl="$(STAGING_DIR)/usr" \
	--enable-shared \
	--disable-g711-codec \
	--disable-g722-codec \
	--disable-g7221-codec \
	--disable-resample \
	--disable-libwebrtc \
	--disable-speex-aec \
	--disable-speex-codec \
	--with-external-srtp="$(STAGING_DIR)/usr" \
	--disable-libyuv \
	--disable-ilbc-codec

TARGET_CFLAGS+=$(TARGET_CPPFLAGS)

define Build/Compile
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)
endef

PJPROJECT_LIBS:= \
	libpj libpjlib-util libpjmedia libpjnath libpjsip-simple \
	libpjsip-ua libpjsip libpjsua libpjsua2

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{include,lib}
	
	$(CP) -R $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include

	$(foreach m,$(PJPROJECT_LIBS),$(CP) $(PKG_INSTALL_DIR)/usr/lib/$(m)* $(1)/usr/lib;)

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(SED) 's|$(TARGET_CFLAGS)||g' $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libpjproject.pc
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libpjproject.pc $(1)/usr/lib/pkgconfig
endef

define Package/libpjmedia
  $(call Package/pjproject/Default)
  TITLE:=libpjmedia library
  DEPENDS+=+libpj +libpjlib-util +libpjnath +librt +libsrtp2
endef

define Package/libpjmedia/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgsmcodec.* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpjmedia.so* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpjmedia-audiodev.so* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpjmedia-codec.so* $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libpjmedia-videodev.so* $(1)/usr/lib
endef

$(eval $(call BuildPackage,libpjmedia))

$(eval $(call PJSIPpackage,libpj,libpj,+librt))
$(eval $(call PJSIPpackage,libpjlib-util,libpjlib-util,+libpj +librt))
$(eval $(call PJSIPpackage,libpjnath,libpjnath,+libpj +libpjlib-util +librt))
$(eval $(call PJSIPpackage,libpjsip-simple,libpjsip-simple,+libpj +libpjlib-util +libpjsip +librt))
$(eval $(call PJSIPpackage,libpjsip-ua,libpjsip-ua,+libpj +libpjlib-util +libpjmedia +libpjsip-simple +libpjsip +librt))
$(eval $(call PJSIPpackage,libpjsip,libpjsip,+libpj +libpjmedia +libpjlib-util +librt +libsrtp2))
$(eval $(call PJSIPpackage,libpjsua,libpjsua,+libpj +libpjlib-util +libpjmedia +libpjnath +libpjsip-simple +libpjsip-ua +libpjsip +librt))
$(eval $(call PJSIPpackage,libpjsua2,libpjsua2,+libpj +libpjlib-util +libpjmedia +libpjnath +libpjsip-simple +libpjsip-ua +libpjsip +librt +libpjsua))
