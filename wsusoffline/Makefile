PACKAGE_ID				= wsusoffline
PACKAGE_NAME			= WSUS Offline Update
PACKAGE_VERSION			= 1
PACKAGE_DESCRIPTION		= Update
VERSION					= 9.7

TARGET					= $(PACKAGE_ID)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: build install clean

build:
	sed -e's/<VERSION>/$(VERSION)/g' -e's/<PACKAGE_VERSION>/$(PACKAGE_VERSION)/g' -e's/<PACKAGE_ID>/$(PACKAGE_ID)/g' -e's/<PACKAGE_DESCRIPTION>/$(PACKAGE_DESCRIPTION)/g' -e's/<PACKAGE_NAME>/$(PACKAGE_NAME)/g' OPSI/control.template > OPSI/control
	opsi-makeproductfile

install:
	opsi-package-manager --install --setup $(TARGET)

clean:
	rm -f $(TARGET)
	rm -rf CLIENT_DATA/files
	rm  OPSI/control

