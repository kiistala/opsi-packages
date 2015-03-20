WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= media-player-classic
PACKAGE_VERSION			= 1
VERSION					= 1.7.8

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_32			= http://downloads.sourceforge.net/project/mpc-hc/MPC%20HomeCinema%20-%20Win32/MPC-HC_v$(VERSION)_x86/MPC-HC.$(VERSION).x86.exe
DOWNLOAD_URL_64			= http://downloads.sourceforge.net/project/mpc-hc/MPC%20HomeCinema%20-%20x64/MPC-HC_v$(VERSION)_x64/MPC-HC.$(VERSION).x64.exe

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_32)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_64)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/MPC-HC.$(VERSION).x86.exe CLIENT_DATA/files/setup_x86.exe
	cp $(DOWNLOAD_DIR)/MPC-HC.$(VERSION).x64.exe CLIENT_DATA/files/setup_x64.exe
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

