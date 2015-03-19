WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= cdburnerxp
PACKAGE_VERSION			= 1
VERSION					= 4.5.4.5306

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_32			= http://download.cdburnerxp.se/msi/cdbxp_setup_$(VERSION).msi
DOWNLOAD_URL_64			= http://download.cdburnerxp.se/msi/cdbxp_setup_x64_$(VERSION).msi

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_32)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_64)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/cdbxp_setup_$(VERSION).msi CLIENT_DATA/files/setup_x86.msi
	cp $(DOWNLOAD_DIR)/cdbxp_setup_x64_$(VERSION).msi CLIENT_DATA/files/setup_x64.msi
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

