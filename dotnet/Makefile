WGET_COMMON_OPTIONS  = -q -N

PACKAGE_NAME         = dotnet
VERSION              = 4.5.2
PACKAGE_VERSION		 = 2

DOWNLOAD_DIR         = ./tmp
DOWNLOAD_URL_1       = http://download.microsoft.com/download/E/2/1/E21644B5-2DF2-47C2-91BD-63C560427900/NDP452-KB2901907-x86-x64-AllOS-ENU.exe
DOWNLOAD_URL_2       = http://download.microsoft.com/download/E/4/E/E4EB40BB-2428-4278-B897-2961E970CF23/NDP452-KB2901907-x86-x64-AllOS-DEU.exe

TARGET               = $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: download build install clean

download:
	mkdir -p $(DOWNLOAD_DIR)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_1)
	wget $(WGET_COMMON_OPTIONS) -P $(DOWNLOAD_DIR) $(DOWNLOAD_URL_2)
	mkdir -p CLIENT_DATA/files
	cp $(DOWNLOAD_DIR)/NDP452-KB2901907-x86-x64-AllOS-ENU.exe CLIENT_DATA/files/setup_1.exe
	cp $(DOWNLOAD_DIR)/NDP452-KB2901907-x86-x64-AllOS-DEU.exe CLIENT_DATA/files/setup_2.exe
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
