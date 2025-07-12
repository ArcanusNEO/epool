MAKEFLAGS += -r
.PHONY: all clean
.SUFFIXES: .c .o .d
SRC := epool.c
OBJ := $(patsubst %.c, %.o, $(SRC))
DEP := $(patsubst %.c, %.d, $(SRC))

CFLAGS ?= -O2 -fno-plt -pipe -flto=auto
CFLAGS += -Wall -Wvla
LDFLAGS ?= -Wl,-O1

all: libepool.so

libepool.so: $(OBJ)
	$(LINK.o) -shared $^ $(LOADLIBES) $(LDLIBS) -o $@

.c.o:
	$(COMPILE.c) -fPIC $< -o $@

clean:
	$(RM) -- $(OBJ) $(DEP) libepool.so

-include $(DEP)
%.d: %.c cmacs.h
	$(COMPILE.c) -MM $< -o $@

cmacs.h:
	$(RM) -- $@
	@wget -qc --show-progress -t 3 --waitretry=3 -O $@ https://raw.githubusercontent.com/ArcanusNEO/cmacs/master/cmacs.h

.SECONDARY: $(OBJ)
