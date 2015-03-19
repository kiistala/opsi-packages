WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= mp3tag
PACKAGE_VERSION			= 1
VERSION					= 2.69

DOWNLOAD_VERSION		= 269
DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL			= http://download.mp3tag.de/mp3tagv$(DOWNLOAD_VERSION)setup.exe

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/mp3tagv$(DOWNLOAD_VERSION)setup.exe CLIENT_DATA/files/setup.exe
	cp CLIENT_DATA/data/Mp3tagSetup.ini CLIENT_DATA/files
	rm -rf $(DOWNLOAD_DIR)

build:
	sed -e's/<VERSION>/$(VERSION)/g' -e's/<PACKAGE_VERSION>/$(PACKAGE_VERSION)/g' OPSI/control.template > OPSI/control
	opsi-makeproductfile

install:
	opsi-package-manager --install --setup $(TARGET)

clean:
	rm -f $(TARGET)
	rm -rf CLIENT_DATA/files 

