LIBSO  := libmylib.so
LIBOBJ := hello.o world.o
OUT    := a.out

CFLAGS  := -I.
LDFLAGS := -L.
LIBS    := -lmylib

CY := '\e[33m'
E  := '\e[0m'

all:
	@echo 'usage:'
	@echo '  make exp'
	@echo '  make clean'

main: lib
	$(CC) main.c $(CFLAGS) $(LDFLAGS) $(LIBS)

lib:
	$(CC) -c -fPIC hello.c world.c
	$(CC) -shared -Wl,-soname,$(LIBSO).1 -o $(LIBSO).1.0.0 $(LIBOBJ)
	ln -sf $(LIBSO).1.0.0 $(LIBSO).1
	ln -sf $(LIBSO).1.0.0 $(LIBSO)

exp: main
	@echo -e $(CY)'libmylib.so.1 => not found'$(E)
	ldd $(OUT)
	@echo -e $(CY)'libmylib.so.1 => ./libmylib.so.1'$(E)
	LD_LIBRARY_PATH=. ldd $(OUT)
	@echo -e $(CY)'error without LD_LIBRARY_PATH set'$(E)
	-./$(OUT)
	@echo -e $(CY)'success'$(OUT)$(E)
	LD_LIBRARY_PATH=. ./$(OUT)

clean:
	rm $(LIBSO).1.0.0 $(LIBSO).1 $(LIBSO) $(LIBOBJ) $(OUT)
