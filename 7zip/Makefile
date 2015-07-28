WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= 7zip
PACKAGE_VERSION			= 1
VERSION					= 15.05

DOWNLOAD_VERSION		= 1505
DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_32			= http://www.7-zip.org/a/7z$(DOWNLOAD_VERSION).exe
DOWNLOAD_URL_64			= http://www.7-zip.org/a/7z$(DOWNLOAD_VERSION)-x64.exe

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_32)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_64)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/7z$(DOWNLOAD_VERSION).exe CLIENT_DATA/files/setup_x86.exe
	cp $(DOWNLOAD_DIR)/7z$(DOWNLOAD_VERSION)-x64.exe CLIENT_DATA/files/setup_x64.exe
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

