WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= google-chrome
PACKAGE_VERSION			= 1
VERSION					= 42.0.2311.152

DOWNLOAD_DIR			= ./tmp
DOWNLOAD_URL_32			= https://dl.google.com/tag/s/appguid%3D%7B8A69D345-D564-463C-AFF1-A69D9E530F96%7D%26iid%3D%7B3A406581-0BD9-9DEA-D2EE-9B69C061D183%7D%26lang%3Dde%26browser%3D3%26usagestats%3D0%26appname%3DGoogle%2520Chrome%26needsadmin%3Dprefers/dl/chrome/install/googlechromestandaloneenterprise.msi
DOWNLOAD_URL_64			= https://dl.google.com/tag/s/appguid%3D%7B8A69D345-D564-463C-AFF1-A69D9E530F96%7D%26iid%3D%7BC2B969B4-7165-E668-7015-8C6AB8EBA708%7D%26lang%3Den%26browser%3D3%26usagestats%3D0%26appname%3DGoogle%2520Chrome%26needsadmin%3Dprefers%26ap%3Dx64-stable/dl/chrome/install/googlechromestandaloneenterprise64.msi

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_32)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_64)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/googlechromestandaloneenterprise.msi CLIENT_DATA/files/setup_x86.msi
	cp $(DOWNLOAD_DIR)/googlechromestandaloneenterprise64.msi CLIENT_DATA/files/setup_x64.msi
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

