CC = gcc
CFLAGS = -Wall
OBJS = libuci2-example.o

all: libuci2-example

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

fbtest: $(OBJS)
	$(CC) -o $@ $(OBJS)

clean:
	rm -f libuci2-example *.o
