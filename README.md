<ul>
<li>step by step install lede luci dan uboot</li>
<pre>
1.install firmware
tanpa password
kita download dulu firmware untuk device anda 
http://felexindo.mooo.com:81
saya pake local
192.168.1.20:81
kita sudah dapat firmwarenya
selanjutnya kita upload ke router
biar mudah menggunakan winscp
saya sudah ada win scp nya 
simpan firmware di folder /tmp
flash firmware clean
mtd -e firmware -r write fw.bin firmware
tunggu sabar
oke install firmware berhasil
kita coba ping 
ping suksess kita masuk ke langkah selanjutnya
setting internet cli wifi 
sebutsaja fdi wifi ap-sta
setelah firmware berhasil kita tidak di tanyakan password 
maka kita buat password dulu terserah anda
ketik 
passwd
2. setting fdi wifi ap-sta
ketik fdi
karakter sensitif perhatikan dengan jelas sebalum menulis
saya pakai FryzilliaZaqhira SSID nya
pilih nomer 3
ketik di router
block info -- untuk melihat terdeteksinya partisi
tunggu sampai connected
suksess
ping facebook.com
ping google.com
ping 8.8.8.8
jika ping domain dan ip berhasil kita bisa langsung tahap exroot
3. exroot
colok flash disk...
buat partisi
EXT4 dan LINUX SWAP
saya sudah buat partisi nya biar singkat waktu
colok kembali ke router flashdisk nya
kita akan membuat exroot di /dev/sda1 dengan partisi ext4
mulain exrootcara clean
mount /dev/sda1 /overlay  <-- putty
rm -rf /overlay/* <-- putty
umount /overlay  <-- putty
fdi  <-- putty
option 1
selesai exroot tapi jangan dulu install apapun kita cek dulu
jika sudah yakin exroot berhasilkita reboot router nya
ketik 
reboot
exroot suksessss
3. install luci
kita lanjut tahap install luci 
agar tidak ada masalah kita cek tahap2 ini
perhatikan
jika sesuai sama dengan di tampilkan kita bisa install luci
option 4
selesai install luci
kita buka browser
luci sudah muncul
suksess
4. wifi web setting cgi html
alternatif setting wifi lewat web
kita test dengan SSID yang sama
masih dalam tahap pengembangan maaf ada banyak bug di sini
mungkin kita kledepannya bikin webui biar lebih kumplit
harap sabar
sudah terkoneksi
skarang kita coba uboot mod pepe2k
5.uboot mod pepe2k
download binary uboot nya
hahaha inggrisnya ngaco
belsambung
semoga berkah amiiin
TEST UBOOT
sambunglan nya belum hehehe
uboot berhasil
terimakasih
</pre>
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
</li>
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
