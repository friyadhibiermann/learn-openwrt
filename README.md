<ul>
<li>
<a>important sed script</a>
</li>
<pre>
sed -e '/sip/ s/^#*/# /' -i test.txt
sed -E 's/( )+$//'
</pre>
<li>
<a>makefile compile</a>
</li>
<pre>
compile:
	CC="$(CC)" CFLAGS="-Os -pipe -mips32r2 -mtune=mips32r2" shc -r -B -f fdi.sh
	CC="$(CC)" CFLAGS="-Os -pipe -mips32r2 -mtune=mips32r2" shc -r -B -f html

	mv fdi.sh.x fdi && mv html.x html && rm *.x.c

clean:

	rm -rf *.x *.c *.o *.c fdi html
</pre>
<li>
<a>compile bash script makefile<>	
</li>
<pre>
include $(TOPDIR)/rules.mk

PKG_NAME:=fdi
PKG_RELEASE:=1.0.2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Package/fdi
  SECTION:=shcbash
  CATEGORY:=shc bash
  SUBMENU :=fdi
  TITLE:=shc script
  DEPENDS :=
endef

define Package/fdi/description
	shc bash compile
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS)
endef

define Package/fdi/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/www/cgi-bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fdi $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/html $(1)/www/cgi-bin/
endef

$(eval $(call BuildPackage,fdi))
</pre>
<li>
<a>makefile include lib and cmake</a>
</li>
<pre>
include $(TOPDIR)/rules.mk

PKG_NAME:=tun2socks
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_INSTALL_DIR:=$(PKG_BUILD_DIR)/ipkg-install

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Package/tun2socks
	SECTION:=tun2socks
	CATEGORY:=WRTnode
	SUBMENU :=opencv_script
	TITLE:=opencv socket
	DEPENDS :=
endef

define Package/tun2socks/description
	opencv trough TCP/IP program for opencv lib
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)/build
	mkdir -p $(PKG_BUILD_DIR)/build
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	cd $(PKG_BUILD_DIR)/build
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		CFLAGS="$(TARGET_CFLAGS)"
endef

define Package/tun2socks/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/tun2socks $(1)/usr/bin/
endef

$(eval $(call BuildPackage,tun2socks))
</pre>
<li>
<a>default /etc/hosts</a>
<li>
<pre>
127.0.0.1 localhost
::1       localhost localhost6 ip6-localhost
#
# Some programs look for these and nice to have in logs
#
fe00::    ip6-localnet
ff00::    ip6-mcastprefix
ff02::1   ip6-allnodes
ff02::2   ip6-allrouters
ff02::3   ip6-allhosts
</pre>
</ul>
