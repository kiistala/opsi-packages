WGET_COMMON_OPTIONS		= -q -N

PACKAGE_NAME			= htpc
PACKAGE_VERSION			= 2
VERSION					= 1.0

TARGET					= $(PACKAGE_NAME)_$(VERSION)-$(PACKAGE_VERSION).opsi

all: build install clean

build:
	sed -e's/<VERSION>/$(VERSION)/g' -e's/<PACKAGE_VERSION>/$(PACKAGE_VERSION)/g' OPSI/control.template > OPSI/control
	opsi-makeproductfile

install:
	opsi-package-manager --install --setup $(TARGET)

clean:
	rm -f $(TARGET)
	rm  OPSI/control


