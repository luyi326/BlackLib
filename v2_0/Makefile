# ;
# Makefile:
# Try to make this library slightly better and installable
# This file is copied from WiringPi
#################################################################################

DYN_VERS_MAJ=2
DYN_VERS_MIN=0

VERSION=$(DYN_VERS_MAJ).$(DYN_VERS_MIN)
DESTDIR=/usr
PREFIX=/local

STATIC=libblackLib.a
DYNAMIC=libblackLib.so.$(VERSION)

#DEBUG	= -g -O0
DEBUG	= -O2
CC	= g++
INCLUDE	= -I.
DEFS	= -D_GNU_SOURCE
CFLAGS	= $(DEBUG) $(DEFS) -std=gnu++0x -Wformat=2 -Wall -Winline $(INCLUDE) -pipe -fPIC

LIBS    =

# Should not alter anything below this line
###############################################################################

SRC	=	BlackADC.cpp BlackCore.cpp				\
		BlackGPIO.cpp BlackI2C.cpp				\
		BlackPWM.cpp BlackSPI.cpp				\
		BlackADC.cpp BlackCore.cpp				\
		BlackUART.cpp

OBJ	=	$(SRC:.c=.o)

all:		$(DYNAMIC)

static:		$(STATIC)

$(STATIC):	$(OBJ)
	@echo "[Link (Static)]"
	@ar rcs $(STATIC) $(OBJ)
	@ranlib $(STATIC)
#	@size   $(STATIC)

$(DYNAMIC):	$(OBJ)
	@echo "[Link (Dynamic)]"
	@$(CC) -shared -Wl,-soname,libblackLib.so -o libblackLib.so.$(VERSION) -lpthread $(OBJ)

.c.o:
	@echo [Compile] $<
	@$(CC) -c $(CFLAGS) $< -o $@

.PHONEY:	clean
clean:
	@echo "[Clean]"
	@rm -f $(OBJ) $(OBJ_I2C) *~ core tags Makefile.bak libblackLib.*

.PHONEY:	tags
tags:	$(SRC)
	@echo [ctags]
	@ctags $(SRC)


.PHONEY:	install-headers
install-headers:
	@echo "[Install Headers]"
	@install -m 0755 -d			$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackLib.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackADC.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackCore.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackDef.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackErr.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackGPIO.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackI2C.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackPWM.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackSPI.h		$(DESTDIR)$(PREFIX)/include
	@install -m 0644 BlackUART.h		$(DESTDIR)$(PREFIX)/include

.PHONEY:	install
install:	$(DYNAMIC) install-headers
	@echo "[Install Dynamic Lib]"
	@install -m 0755 -d						$(DESTDIR)$(PREFIX)/lib
	@install -m 0755 libblackLib.so.$(VERSION)			$(DESTDIR)$(PREFIX)/lib/libblackLib.so.$(VERSION)
	@ln -sf $(DESTDIR)$(PREFIX)/lib/libblackLib.so.$(VERSION)	$(DESTDIR)/lib/libblackLib.so
	@ldconfig

.PHONEY:	install-static
install-static:	$(STATIC) install-headers
	@echo "[Install Static Lib]"
	@install -m 0755 -d			$(DESTDIR)$(PREFIX)/lib
	@install -m 0755 libblackLib.a		$(DESTDIR)$(PREFIX)/lib

.PHONEY:	uninstall
uninstall:
	@echo "[UnInstall]"
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackLib.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackADC.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackCore.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackDef.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackErr.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackGPIO.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackI2C.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackPWM.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackSPI.h
	@rm -f $(DESTDIR)$(PREFIX)/include/BlackUART.h
	@rm -f $(DESTDIR)$(PREFIX)/lib/libblackLib.*
	@ldconfig


.PHONEY:	depend
depend:
	makedepend -Y $(SRC) $(SRC_I2C)

# DO NOT DELETE

BlackLib.o: BlackCore.h BlackADC.h BlackPWM.h BlackGPIO.h BlackUART.h BlackSPI.h BlackI2C.h
BlackADC.o: BlackCore.h
BlackCore.o: BlackErr.h BlackDef.h
BlackGPIO.o: BlackCore.h
BlackI2C.o: BlackCore.h
BlackPWM.o: BlackCore.h
BlackSPI.o: BlackCore.h
BlackUART.o: BlackCore.h
