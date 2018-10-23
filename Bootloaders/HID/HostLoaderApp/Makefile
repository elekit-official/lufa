#OS ?= LINUX
#OS ?= WINDOWS
OS ?= MACOSX
#OS ?= BSD

ifeq ($(OS), LINUX)  # also works on FreeBSD
CC ?= gcc
CFLAGS ?= -O2 -Wall
hid_bootloader_cli_linux_x86: hid_bootloader_cli.c
	$(CC) $(CFLAGS) -s -DUSE_LIBUSB -o $@ $^ -lusb


else ifeq ($(OS), WINDOWS)
CC = gcc
#CC = i586-mingw32msvc-gcc
CFLAGS ?= -O2 -Wall
LDLIB = -lsetupapi -lhid
hid_bootloader_cli.exe: hid_bootloader_cli.c
	$(CC) $(CFLAGS) -s -DUSE_WIN32 -o $@ $^ $(LDLIB)


else ifeq ($(OS), MACOSX)
CC ?= gcc
SDK ?= /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk
#SDK ?= /Developer/SDKs/MacOSX10.5.sdk
CFLAGS ?= -O2 -Wall
hid_bootloader_cli_macosx: hid_bootloader_cli.c
	$(CC) $(CFLAGS) -DUSE_APPLE_IOKIT -isysroot $(SDK) -o $@ $^ -Wl,-syslibroot,$(SDK) -framework IOKit -framework CoreFoundation


else ifeq ($(OS), BSD)  # works on NetBSD and OpenBSD
CC ?= gcct
CFLAGS ?= -O2 -Wall
hid_bootloader_cli: hid_bootloader_cli.c
	$(CC) $(CFLAGS) -s -DUSE_UHID -o hid_bootloader_cli hid_bootloader_cli.c


endif


clean:
	rm -f hid_bootloader_cli_macosx hid_bootloader_cli_linux_x86 hid_bootloader_cli.exe
