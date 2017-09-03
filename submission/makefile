.PHONY: all clean

all: hello mystery-valentine

hello: hello.c
	gcc -o hello hello.c

mystery-valentine: mystery-valentine.c
	gcc -o mystery-valentine mystery-valentine.c

run: hello mystery-valentine
	./hello
	./mystery-valentine

clean:
	rm -f hello
	rm -f mystery-valentine
