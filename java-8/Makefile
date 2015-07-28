PACKAGE_ID				= java-8
PACKAGE_NAME			= Oracle JAVA
PACKAGE_VERSION			= 1
PACKAGE_DESCRIPTION		= Oracle JAVA
VERSION					= 8.51

TARGET					= $(PACKAGE_ID)_$(VERSION)-$(PACKAGE_VERSION).opsi

WGET_COMMON_OPTIONS		= -q -N
DOWNLOAD_VERSION		= 8.0_51
DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_32			= https://github.com/astrapi/opsi-packages-bin/raw/master/java/java-8/jre1.$(DOWNLOAD_VERSION).msi
DOWNLOAD_URL_64			= https://github.com/astrapi/opsi-packages-bin/raw/master/java/java-8/jre1.$(DOWNLOAD_VERSION)-x64.msi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_32)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_64)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/jre1.$(DOWNLOAD_VERSION).msi CLIENT_DATA/files/setup_x86.msi
	cp $(DOWNLOAD_DIR)/jre1.$(DOWNLOAD_VERSION)-x64.msi CLIENT_DATA/files/setup_x64.msi
	rm -rf $(DOWNLOAD_DIR)

build:
	sed -e's/<VERSION>/$(VERSION)/g' -e's/<PACKAGE_VERSION>/$(PACKAGE_VERSION)/g' -e's/<PACKAGE_ID>/$(PACKAGE_ID)/g' -e's/<PACKAGE_DESCRIPTION>/$(PACKAGE_DESCRIPTION)/g' -e's/<PACKAGE_NAME>/$(PACKAGE_NAME)/g' OPSI/control.template > OPSI/control
	opsi-makeproductfile

install:
	opsi-package-manager --install --setup $(TARGET)

clean:
	rm -f $(TARGET)
	rm -rf CLIENT_DATA/files
	rm  OPSI/control

