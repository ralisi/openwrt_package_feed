# 
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 13562 2008-12-09 10:32:28Z jow $

include $(TOPDIR)/rules.mk

PKG_NAME:=olsrd-cl
PKG_VERSION:=0.5.6_a
PKG_RELEASE:=2
PKG_REV:=bdebcfe09159b7a75813debf2951dc4c87e1d967


PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=olsrd-cl-$(PKG_VERSION)
PKG_SOURCE_URL:=git://github.com/ralisi/olsrd_cl_roam.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += $(FPIC)

define Package/olsrd-cl/template
  SECTION:=net
  CATEGORY:=Network
  TITLE:=OLSRd with clientroaming
  URL:=http://www.olsr.org/
endef

define Package/olsrd-cl
  $(call Package/olsrd-cl/template)
  MENU:=1
  DEPENDS:=+libpthread
endef

define Package/olsrd-cl/conffiles
/etc/config/olsrd
endef

define Package/olsrd-cl-mod-arprefresh
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Kernel ARP cache refresh plugin
endef

define Package/olsrd-cl-mod-dot-draw
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Dot topology information plugin
endef

define Package/olsrd-cl-mod-bmf
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl +kmod-tun
  TITLE:=Basic multicast forwarding plugin
endef

define Package/olsrd-cl-mod-dyn-gw
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Dynamic internet gateway plugin
endef

define Package/olsrd-cl-mod-dyn-gw-plain
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Dynamic internet gateway plain plugin
endef

define Package/olsrd-cl-mod-httpinfo
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Small informative web server plugin
endef

define Package/olsrd-cl-mod-nameservice
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Lightweight hostname resolver plugin
endef

define Package/olsrd-cl-mod-secure
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Message signing plugin to secure routing domain
endef

define Package/olsrd-cl-mod-txtinfo
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl
  TITLE:=Small informative web server plugin
endef

define Package/olsrd-cl-mod-cl_roam
  $(call Package/olsrd-cl/template)
  DEPENDS:=olsrd-cl +wget
  TITLE:=Enables client-roaming
endef

define Package/olsrd-cl-mod-secure/conffiles
/etc/olsrd.d/olsrd_secure_key
endef

define Build/Configure
endef

define Build/Compile
	rm -rf $(PKG_INSTALL_DIR)
	mkdir -p $(PKG_INSTALL_DIR)
	$(MAKE) -C "$(PKG_BUILD_DIR)" \
		$(TARGET_CONFIGURE_OPTS) \
		NODEBUG=1 \
		CFLAGS="$(TARGET_CFLAGS)" \
		OS="linux" \
		INSTALL_PREFIX="$(PKG_INSTALL_DIR)" \
		LIBDIR="$(PKG_INSTALL_DIR)/usr/lib" \
		SBINDIR="$(PKG_INSTALL_DIR)/usr/sbin/" \
		ETCDIR="$(PKG_INSTALL_DIR)/etc" \
		MANDIR="$(PKG_INSTALL_DIR)/usr/share/man" \
		STRIP="true" \
		INSTALL_LIB="true" \
		SUBDIRS="arprefresh bmf dot_draw dyn_gw dyn_gw_plain httpinfo nameservice secure txtinfo cl_roam" \
		all libs install install_libs
endef

define Package/olsrd-cl/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/olsrd.config $(1)/etc/config/olsrd
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/olsrd $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/olsrd.init $(1)/etc/init.d/olsrd
endef

define Package/olsrd-cl-mod-arprefresh/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/arprefresh/olsrd_arprefresh.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-dot-draw/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/dot_draw/olsrd_dot_draw.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-bmf/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/bmf/olsrd_bmf.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-dyn-gw/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/dyn_gw/olsrd_dyn_gw.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-dyn-gw-plain/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/dyn_gw_plain/olsrd_dyn_gw_plain.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-httpinfo/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/httpinfo/olsrd_httpinfo.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-nameservice/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/nameservice/olsrd_nameservice.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-cl_roam/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/cl_roam/olsrd_cl_roam.so.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/www
	ln -sf /var/dhcp.leases $(1)/www/dhcp.leases
endef

define Package/olsrd-cl-mod-secure/install
	$(INSTALL_DIR) $(1)/etc/olsrd.d
	$(CP) ./files/olsrd_secure_key $(1)/etc/olsrd.d/
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/secure/olsrd_secure.so.* $(1)/usr/lib/
endef

define Package/olsrd-cl-mod-txtinfo/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/txtinfo/olsrd_txtinfo.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,olsrd-cl))
$(eval $(call BuildPackage,olsrd-cl-mod-arprefresh))
$(eval $(call BuildPackage,olsrd-cl-mod-dot-draw))
$(eval $(call BuildPackage,olsrd-cl-mod-bmf))
$(eval $(call BuildPackage,olsrd-cl-mod-dyn-gw))
$(eval $(call BuildPackage,olsrd-cl-mod-dyn-gw-plain))
$(eval $(call BuildPackage,olsrd-cl-mod-httpinfo))
$(eval $(call BuildPackage,olsrd-cl-mod-nameservice))
$(eval $(call BuildPackage,olsrd-cl-mod-secure))
$(eval $(call BuildPackage,olsrd-cl-mod-txtinfo))
$(eval $(call BuildPackage,olsrd-cl-mod-cl_roam))
