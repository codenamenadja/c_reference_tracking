CFLAGS= -Werror -Wextra -Wall -Iincludes/ 
LIBS= -ldl $(OPTLIBS)
PREFIX?= ./

SOURCES= $(wildcard src/*.c)
OBJECTS= $(patsubst %.c,%.o,$(SOURCES))

TARGET= d_lib.a
SO_TARGET= $(patsubst %.a, %.so, $(TARGET))
TEST_SRC = main.c

.PHONY: all
all: $(TARGET) $(SO_TARGET)

$(TARGET): CFLAGS += -fPIC
$(TARGET): $(OBJECTS)
	ar rcs $@ $(OBJECTS)
	ranlib $@

$(SO_TARGET): $(OBJECTS)
	$(CC) -shared -o $@ $(OBJECTS)

.PHONY: clean
clean:
	rm -rf $(OBJECTS) $(TARGET)

.PHONY: fclean
fclean:
	rm -rf $(TARGET) $(SO_TARGET)

.PHONY: test
test:
	$(CC) $(CFLAGS) $(TEST_SRC) -ldl -o main.out
