WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= notepadpp
PACKAGE_VERSION			= 1
VERSION				= 6.7.9.2

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL			= https://notepad-plus-plus.org/repository/6.x/$(VERSION)/npp.$(VERSION).Installer.exe

TARGET				= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/npp.$(VERSION).Installer.exe CLIENT_DATA/files/setup.exe
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

