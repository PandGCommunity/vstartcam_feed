include $(TOPDIR)/rules.mk

PKG_NAME:=rt5350f-wm8988
PKG_RELEASE:=1

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_MAINTAINER:=Sergey Sharshunov <s.sharshunov@gmail.com>
PKG_BUILD_PARALLEL:=1

PKG_CONFIG_DEPENDS += \
	CONFIG_PACKAGE_kmod-sound-rt5350f-wm8988

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/sound-rt5350f-wm8988
	SUBMENU:=Sound Support
	TITLE:=RT5350F WM8988 ALSA SoC Machine Driver
	KCONFIG:= CONFIG_SND_SOC_WM8988 \
		CONFIG_SND_RALINK_SOC_I2S
	DEPENDS:=@TARGET_ramips +kmod-sound-soc-core \
		+!(TARGET_ramips_rt305x):+kmod-regmap +kmod-dma-ralink \
		@!TARGET_ramips_rt288x
	FILES:=$(PKG_BUILD_DIR)/snd-soc-rt5350f-wm8988.ko \
		$(LINUX_DIR)/sound/soc/ralink/snd-soc-ralink-i2s.ko \
		$(LINUX_DIR)/sound/soc/codecs/snd-soc-wm8988.ko
	AUTOLOAD:=$(call AutoLoad,91,snd-soc-ralink-i2s snd-soc-wm8988 snd-soc-rt5350f-wm8988)
endef

# define KernelPackage/sound-rt5350f-wm8988
# 	SUBMENU:=Sound Support
# 	TITLE:=RT5350F WM8988 ALSA SoC Machine Driver
# 	KCONFIG:= \
# 	CONFIG_SND_SOC_WM8988
# 	DEPENDS:=@TARGET_ramips +kmod-sound-soc-core \
# 		+!(TARGET_ramips_rt305x):+kmod-regmap +kmod-dma-ralink \
# 		@!TARGET_ramips_rt288x
# 	FILES:= \
# 	$(LINUX_DIR)/sound/soc/codecs/snd-soc-wm8988.ko \
# 	$(PKG_BUILD_DIR)/snd-soc-rt5350f-wm8988.ko
# 	AUTOLOAD:=$(call AutoLoad,91,snd-soc-wm8988 snd-soc-rt5350f-wm8988)
# endef

# DEPENDS:=@TARGET_ramips +kmod-sound-mt7620 \
# 		+!(TARGET_ramips_rt305x):kmod-i2c-ralink \
# 		@!TARGET_ramips_rt288x

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(LINUX_DIR)/sound/soc/ralink

ifdef CONFIG_PACKAGE_kmod-sound-rt5350f-wm8988
	PKG_MAKE_FLAGS += CONFIG_SND_SOC_RT5350F_WM8988=m
endif

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		$(PKG_MAKE_FLAGS) \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef

define Package/kmod-sound-rt5350f-wm8988/install
	true
endef

# define KernelPackage/sound-rt5350f-wm8988/install
# 	$(INSTALL_DIR) $(1)/etc
# 	$(CP) $(PKG_BUILD_DIR)/asound.conf $(1)/etc/asound.conf
# endef
# $(CP) $(PKG_BUILD_DIR)/examples/asound.conf.alsa $(1)/etc/asound.conf
$(eval $(call KernelPackage,sound-rt5350f-wm8988))
