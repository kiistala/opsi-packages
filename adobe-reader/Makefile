WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= adobe-reader
PACKAGE_VERSION			= 1
VERSION					= 11.0.10

DOWNLOAD_VERSION		= 11010
DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL			= ftp://ftp.adobe.com/pub/adobe/reader/win/11.x/$(VERSION)/de_DE/AdbeRdr$(DOWNLOAD_VERSION)_de_DE.exe

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/AdbeRdr$(DOWNLOAD_VERSION)_de_DE.exe CLIENT_DATA/files/setup.exe
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


