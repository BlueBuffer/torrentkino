export CODENAME = libnss_tk6.so.2
export CC = gcc
export CFLAGS = -O2
CFLAGS += -std=gnu99 -fPIC -DPIC
CFLAGS += -Wall -Wwrite-strings -pedantic
CFLAGS += -DTORRENTKINO -DNSS -DIPV6
export LDFLAGS = -lpthread
OBJS=nss.o str.o malloc.o fail.o client.o ip.o

.PHONY: all clean install

all: $(CODENAME)

%.o : ../src/nss/%.c ../src/nss/%.h
	$(CC) $(CFLAGS) -c $<

%.o : ../src/shr/%.c ../src/shr/%.h
	$(CC) $(CFLAGS) -c $<

%.o : ../src/dns/%.c ../src/dns/%.h
	$(CC) $(CFLAGS) -c $<

$(CODENAME): $(OBJS)
	$(CC) $(CFLAGS) -shared -Wl,-soname,$(CODENAME) $(OBJS) -o $(CODENAME) $(LDFLAGS)

clean:
	rm -f *.o $(CODENAME)

install:
	strip $(CODENAME)
	mkdir -p $(DESTDIR)/lib/$(DEB_HOST_MULTIARCH)/
	cp $(CODENAME) $(DESTDIR)/lib/$(DEB_HOST_MULTIARCH)/
