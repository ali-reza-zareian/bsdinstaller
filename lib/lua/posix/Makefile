# makefile for POSIX library for Lua

BASE?=../../..
include ${BASE}/Config

# change these to reflect your Lua installation
LUA= ../../../lua
LUAINC= $(LUA)/include
LUALIB= $(LUA)/lib
LUABIN= $(LUA)/bin

COMPAT=../compat-5.1

MYNAME= posix
MYLIB= l$(MYNAME)

# no need to change anything below here
CFLAGS+= -fPIC -O2 -pedantic -Wall -I$(LUAINC)
LDFLAGS+=-L$(LUALIB) -L/usr/local/lib -llua50 -llualib50

OBJS= $(MYLIB).o

T= $(MYLIB).so

all:	$T

strip:
	strip $T

$T:	$(OBJS)
	$(CC) -fPIC $(OBJS) $(COMPAT)/compat-5.1.o -shared $(LDFLAGS) -o $@

$(OBJS): modemuncher.c

clean:
	rm -f $(OBJS) $T core core.* a.out

x:
	@echo "$(MYNAME) library:"
	@grep '},' $(MYLIB).c | cut -f2 | tr -d '{",' | sort | column

xx:
	@echo "$(MYNAME) library:"
	@fgrep '/**' $(MYLIB).c | cut -f2 -d/ | tr -d '*' | sort | column

# distribution

install: strip
	mkdir -p $(DESTDIR)${PREFIX}/lib/lua/5.0
	cp $T $(DESTDIR)${PREFIX}/lib/lua/5.0
	mkdir -p ${DESTDIR}${PREFIX}/share/lua/5.0
	cp posix.lua ${DESTDIR}${PREFIX}/share/lua/5.0

# eof
