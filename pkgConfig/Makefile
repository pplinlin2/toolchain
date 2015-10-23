LIBSO  := libmylib.so
LIBOBJ := hello.o world.o
OUT    := a.out

CY := '\e[33m'
E  := '\e[0m'

all:
	@echo 'usage:'
	@echo '  make exp'
	@echo '  make clean'

main: lib
	export PKG_CONFIG_PATH=. && \
	$(CC) main.c `pkg-config --cflags --libs mylib`

lib:
	$(CC) -c -fPIC hello.c world.c
	$(CC) -shared -Wl,-soname,$(LIBSO).1 -o $(LIBSO).1.0.0 $(LIBOBJ)
	ln -sf $(LIBSO).1.0.0 $(LIBSO).1
	ln -sf $(LIBSO).1.0.0 $(LIBSO)

exp: main
	@echo -e $(CY)'pkg-config verification'$(E)
	PKG_CONFIG_PATH=. pkg-config mylib --libs
	PKG_CONFIG_PATH=. pkg-config mylib --cflags
	PKG_CONFIG_PATH=. pkg-config mylib --modversion
	LD_LIBRARY_PATH=. ./$(OUT)

clean:
	rm $(LIBSO).1.0.0 $(LIBSO).1 $(LIBSO) $(LIBOBJ) $(OUT)
