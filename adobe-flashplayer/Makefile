WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= adobe-flashplayer
PACKAGE_VERSION			= 1
VERSION				= 17.0.0.169

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_1			= http://download.macromedia.com/get/flashplayer/current/licensing/win/install_flash_player_17_active_x.msi
DOWNLOAD_URL_2			= http://download.macromedia.com/get/flashplayer/current/licensing/win/install_flash_player_17_plugin.msi

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_1)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_2)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/install_flash_player_17_active_x.msi CLIENT_DATA/files/setup_1.msi
	cp $(DOWNLOAD_DIR)/install_flash_player_17_plugin.msi CLIENT_DATA/files/setup_2.msi
	rm -rf $(DOWNLOAD_DIR)

build:
	sed -e's/<VERSION>/$(VERSION)/g' -e's/<PACKAGE_VERSION>/$(PACKAGE_VERSION)/g' OPSI/control.template > OPSI/control
	opsi-makeproductfile

install:
	opsi-package-manager --install --setup $(TARGET)

clean:
	rm -f $(TARGET)
	rm -rf CLIENT_DATA/files
	rm  OPSI/control


