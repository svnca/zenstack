TOPDIR=..

ifeq ($(FF_PATH),)
	FF_PATH=${TOPDIR}
endif

# ifneq ($(shell pkg-config --exists libdpdk && echo 0),0)
# $(error "No installation of DPDK found, maybe you should export environment variable `PKG_CONFIG_PATH`")
# endif

PKGCONF ?= pkg-config

CFLAGS += -O0 -g -gdwarf-2 -I$(TOPDIR)/lib

LIBS+= $(shell $(PKGCONF) --static --libs libdpdk)
# LIBS+= -L${FF_PATH}/lib -Wl,--whole-archive,-lfstack,--no-whole-archive
# LIBS+= -Wl,--no-whole-archive -lrt -lm -ldl -lcrypto -pthread
LIBS+= -L${FF_PATH}/lib -lfstack
LIBS+= -lrt -lm -ldl -lcrypto -pthread

TARGET="helloworld"
all:
	@echo "topdir: $(TOPDIR)"
	# @echo "ls topdir"
	# @echo "------------"
	# @ls $(TOPDIR)/lib
	@echo "------------"
	cc ${CFLAGS} -DINET6 -o ${TARGET} main.c ${LIBS}
	cc ${CFLAGS} -o ${TARGET}_epoll main_epoll.c ${LIBS}

.PHONY: clean
clean:
	rm -f *.o ${TARGET} ${TARGET}_epoll
