WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= virtualbox-guest-tools
PACKAGE_VERSION			= 3
VERSION				= 4.3.26

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL			= http://download.virtualbox.org/virtualbox/$(VERSION)/VBoxGuestAdditions_$(VERSION).iso

TARGET				= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL)
	mkdir -p $(DOWNLOAD_DIR)/mount
	fuseiso $(DOWNLOAD_DIR)/VBoxGuestAdditions_$(VERSION).iso $(DOWNLOAD_DIR)/mount
	mkdir -p CLIENT_DATA/files
	rm -f CLIENT_DATA/files/*
	cp $(DOWNLOAD_DIR)/mount/VBoxWindowsAdditions.exe CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/mount/VBoxWindowsAdditions-amd64.exe CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/mount/VBoxWindowsAdditions-x86.exe CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/mount/cert/oracle-vbox.cer CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/mount/cert/VBoxCertUtil.exe CLIENT_DATA/files
	fusermount -u $(DOWNLOAD_DIR)/mount
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

