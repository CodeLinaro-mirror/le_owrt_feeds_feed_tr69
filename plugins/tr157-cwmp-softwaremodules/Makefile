include $(TOPDIR)/rules.mk
-include $(STAGING_DIR)/components.config

PKG_NAME:=tr157-cwmp-softwaremodules
PKG_VERSION:=v0.1.10
SHORT_DESCRIPTION:=tr157-cwmp-softwaremodules

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=v0.1.10
PKG_SOURCE_URL:=https://$(SAH_GIT_USER):$(SAH_GIT_TOKEN)@$(SAH_GIT)/$(SAH_GIT_GROUP)/tr157-cwmp-softwaremodules.git
PKG_MIRROR_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_MAINTAINER:=Soft At Home <support.opensource@softathome.com>
PKG_LICENSE:=BSD-2-Clause-Patent
PKG_LICENSE_FILES:=LICENSE

COMPONENT:=tr157-cwmp-softwaremodules

PKG_RELEASE:=1

define SAHInit/Install
	install -d ${PKG_INSTALL_DIR}/etc/rc.d/
	ln -sfr ${PKG_INSTALL_DIR}/etc/init.d/$(COMPONENT) ${PKG_INSTALL_DIR}/etc/rc.d/S99$(COMPONENT)
	ln -sfr ${PKG_INSTALL_DIR}/etc/init.d/$(COMPONENT) ${PKG_INSTALL_DIR}/etc/rc.d/K99$(COMPONENT)
endef

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  CATEGORY:=amx
  SUBMENU:=TR-181 Managers
  TITLE:=$(SHORT_DESCRIPTION)
  URL:=https://$(SAH_GIT)/$(SAH_GIT_GROUP)/tr157-cwmp-softwaremodules
  DEPENDS += +libamxc
  DEPENDS += +libamxp
  DEPENDS += +libamxj
  DEPENDS += +libamxd
  DEPENDS += +libamxb
  DEPENDS += +libamxo
  DEPENDS += +libsahtrace
  DEPENDS += +mod-dmext
  DEPENDS += +libevent2
  DEPENDS += +libamxm
  DEPENDS += +amxrt
  MENU:=1
endef

define Package/$(PKG_NAME)/description
	tr157-cwmp-softwaremodules
endef

define Build/Compile
	$(call Build/Compile/Default, STAGINGDIR=$(STAGING_DIR) CONFIGDIR=$(STAGING_DIR) PKG_CONFIG_PATH=$(STAGING_DIR)/usr/lib/pkgconfig LIBDIR=/usr/lib INSTALL_LIB_DIR=/lib INSTALL_BIN_DIR=/bin RAW_VERSION=$(PKG_VERSION) HARDCO_HAL_DIR=$(STAGING_DIR)/usr/include CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER=$(CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER))
endef

define Build/Install
	$(call Build/Install/Default, install INSTALL=install D=$(PKG_INSTALL_DIR) DEST=$(PKG_INSTALL_DIR) STAGINGDIR=$(STAGING_DIR) CONFIGDIR=$(STAGING_DIR) PV=$(PKG_VERSION) PKG_CONFIG_LIBDIR=$(STAGING_DIR)/usr/lib/pkgconfig LIBDIR=/usr/lib INSTALL_LIB_DIR=/lib INSTALL_BIN_DIR=/bin RAW_VERSION=$(PKG_VERSION) HARDCO_HAL_DIR=$(STAGING_DIR)/usr/include CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER=$(CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER))

	$(call SAHInit/Install)
endef

define Build/InstallDev
	$(call Build/Install/Default, install INSTALL=install D=$(STAGING_DIR) DEST=$(STAGING_DIR) STAGINGDIR=$(STAGING_DIR) CONFIGDIR=$(STAGING_DIR) PV=$(PKG_VERSION) PKG_CONFIG_LIBDIR=$(STAGING_DIR)/usr/lib/pkgconfig LIBDIR=/usr/lib INSTALL_LIB_DIR=/lib INSTALL_BIN_DIR=/bin RAW_VERSION=$(PKG_VERSION) HARDCO_HAL_DIR=$(STAGING_DIR)/usr/include CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER=$(CONFIG_SAH_SERVICES_TR157_CWMP_SOFTWAREMODULES_DUMMY_CONTROLLER))
endef

define Package/$(PKG_NAME)/install
	$(CP) $(PKG_INSTALL_DIR)/* $(1)/
	if [ -d ./files ]; then \
		$(CP) ./files/* $(1)/; \
	fi
	find $(1) -name *.a -exec rm {} +;
	find $(1) -name *.h -exec rm {} +;
	find $(1) -name *.pc -exec rm {} +;
endef

define Package/$(PKG_NAME)/config
	source "$(SOURCE)/Config.in"
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
