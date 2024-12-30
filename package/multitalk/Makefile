include $(TOPDIR)/rules.mk

PKG_NAME:=multitalk
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/sfiera/multitalk/tar.gz/v${PKG_VERSION}?
PKG_HASH:=84e81ce0e570c93bd2d55aaed89d7c8d976e24805a66219bfc4fcc03ddc722c0

PKG_MAINTAINER:=Peter Godwin <pgodwin@gmail.com>
PKG_LICENSE:=BSD
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/multitalk-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=golang/host 
PKG_BUILD_PARALLEL:=1
PKG_BUILD_FLAGS:=no-mips16
#PKG_INSTALL:=1

GO_PKG:=github.com/sfiera/multitalk

GO_PKG_LDFLAGS_X:=\
	main.version=v$(PKG_VERSION) \
	main.commit=$(PKG_VERSION)  \
	main.builtBy=openwrt \

include $(INCLUDE_DIR)/package.mk
include ../../feeds/packages/lang/golang/golang-package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=MultiTalk
  URL:=https://github.com/sfiera/multitalk
  DEPENDS:=$(GO_ARCH_DEPENDS) +libpthread +libpcap
endef

define Package/$(PKG_NAME)/description
  MultiTalk is a repeater for different transports for AppleTalk:
   - EtherTalk, spoken by Classic MacOS or netatalk2 machines over Ethernet
   - LocalTalk-over-UDP (LToU) multicast, spoken by Mini vMac 37+
   - TCP, spoken between multitalk instances or bbraun's kwai server
   - TashTalk, spoken by TashTalk-programmed PICs over serial
endef

GO_PKG_INSTALL_EXTRA:=Makefile

MAKE_PATH:=$(GO_PKG_WORK_DIR_NAME)/build/src/$(GO_PKG)
MAKE_VARS += $(GO_PKG_VARS)

# Reset golang-package.mk overrides so we can use the Makefile
#Build/Compile=$(call Build/Compile/Default)


define Package/$(PKG_NAME)/install
  $(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/multitalk $(1)/usr/bin/
endef


$(eval $(call BuildPackage,$(PKG_NAME)))