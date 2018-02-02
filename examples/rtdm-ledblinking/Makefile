DEST_DIR=bin
RPI3_ROOTFS_DIR=/home/dmarchal/projects/2018/PADR/sprint/xenomai/XENOMAI_DIR

EXEC=rtdm-ledblinking.exe

CC= arm-linux-gnueabihf-gcc
SRC= rtdm-ledblinking.c
OBJ= $(SRC:.c=.o)
#CFLAGS=-g -W -Wall -I$(RPI3_ROOTFS_DIR)/usr/xenomai/include -D_GNU_SOURCE -D_REENTRANT
CFLAGS=-Wall -W -I$(RPI3_ROOTFS_DIR)/usr/xenomai/include/cobalt -I$(RPI3_ROOTFS_DIR)/usr/xenomai/include/alchemy -I$(RPI3_ROOTFS_DIR)/usr/xenomai/include  -D_GNU_SOURCE -D_REENTRANT -D__COBALT__ -Wl,--wrap=main -Wl,--dynamic-list=$(RPI3_ROOTFS_DIR)/usr/xenomai/lib/dynlist.ld
LDFLAGS=-L$(RPI3_ROOTFS_DIR)/usr/xenomai/lib -lcobalt -lpthread -lrt -lalchemy -lcopperplate $(RPI3_ROOTFS_DIR)/usr/xenomai/lib/xenomai/bootstrap.o

$(EXEC): $(OBJ)
	$(CC) -o $@ $^ $(LDFLAGS)

$(OBJ): $(SRC)
	$(CC) $(CFLAGS) -o $@ -c $<

all: $(EXEC)

clean:
	rm -rf $(OBJ)
	rm -rf $(EXEC)
	rm -f *.c~ *.h~ Makefile~

install: $(EXEC)
	@mkdir ­-p $(DEST_DIR)/$(EXEC)
	echo "$(EXEC):native:!./$(EXEC);popall:control_c" >	$(DEST_DIR)/$(EXEC)/.runinfo
	cp -f $(EXEC) $(DEST_DIR)/$(EXEC)

mrproper: clean
	rm -rf $(DEST_DIR)/$(EXEC)

.PHONY: all install clean mrproper
