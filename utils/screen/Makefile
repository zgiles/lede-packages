#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=screen
PKG_VERSION:=4.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=aba9af66cb626155d6abce4703f45cce0e30a5114a368bd6387c966cbbbb7c64
PKG_SOURCE_URL:=@GNU/screen

PKG_LICENSE:=GPL-3.0+
PKG_LICENSE_FILES:=

include $(INCLUDE_DIR)/package.mk

define Package/screen
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Terminal
  DEPENDS:=+libncurses
  TITLE:=Full-screen terminal window manager
  URL:=http://www.gnu.org/software/screen/
  MAINTAINER:=Etienne CHAMPETIER <champetier.etienne@gmail.com>
endef

define Package/screen/description
	Screen is a full-screen window manager that multiplexes a physical
	terminal between several processes, typically interactive shells.
endef

define Build/Configure
	$(call Build/Configure/Default,\
		--with-sys-screenrc=/etc/screenrc \
		--enable-colors256 \
	)
	# XXX: memmove() works well with overlapped memory areas
	echo "#define USEMEMMOVE 1" >>$(PKG_BUILD_DIR)/config.h
endef

define Package/screen/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/screen $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) ./files/etc/screenrc $(1)/etc/screenrc
endef

define Package/screen/conffiles
/etc/screenrc
endef

$(eval $(call BuildPackage,screen))
