CC ?= gcc

ERTS_INCLUDE_DIR ?= $(shell erl -noshell -s init stop -eval "io:format(\"~s/erts-~s/include/\", [code:root_dir(), erlang:system_info(version)]).")

LDFLAGS += -shared -lcouchbase

CFLAGS += -fPIC -O3 -Wall -isystem $(ERTS_INCLUDE_DIR)

all: ../priv/cberl_drv.so 

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

../priv/cberl_drv.so: callbacks.o cb.o cberl_nif.o queue.o
	$(CC) $? -o $@ $(LDFLAGS)

.PHONY: clean
clean:
	rm -f ../priv/cberl_drv.so *.o
