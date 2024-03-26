CC=gcc
CFLAGS= -Wall -Wextra -Werror -g
OFLAGS= -march=native -mtune=native -O3 -finline-functions -funroll-loops -fpeel-loops -ftree-vectorize -ftree-loop-vectorize
EXE=bench

.PHONY: all clean run

all: build

build: $(EXE)
$(EXE): main.o compute.o vector.o
	$(CC) $(LDFLAGS) $^ -o $@
%.o: %.c
	$(CC) $(CFLAGS) $(OFLAGS) -c $< -o $@

run:
	./$(EXE)

clean: 
	rm *.o
	rm $(EXE)



