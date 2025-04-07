# -- Утилиты

clear:
 rm -rf *.o *.a *_test integral equation list stack

fmt:
 clang-format -style=LLVM -i find -regex ".+\.[ch]"

check_fmt:
 clang-format -style=LLVM -i find -regex ".+\.[ch]" --dry-run --Werror


# -- Сборка статических библиотек

equation.o: equation.c equation.h
 gcc -g -c equation.c -o equation.o -lm

equation.a: equation.o
 ar rc equation.a equation.o -lm


integral.o: integral.c integral.h
 gcc -g -c integral.c -o integral.o -lm

integral.a: integral.o
 ar rc integral.a integral.o -lm


list.o: list.c list.h
 gcc -g -c list.c -o list.o

list.a: list.o
 ar rc list.a list.o


stack.o: stack.c stack.h
 gcc -g -c stack.c -o stack.o

stack.a: stack.o
 ar rc stack.a stack.o


# -- Сборка тестов

equation_test.o: tests/equation_test.c equation.h
 gcc -g -c tests/equation_test.c -o equation_test.o -lm

equation_test: equation_test.o equation.a
 gcc -g -static -o equation_test equation_test.o equation.a -lm


integral_test.o: tests/integral_test.c integral.h
 gcc -g -c tests/integral_test.c -o integral_test.o -lm

integral_test: integral_test.o integral.a
 gcc -g -static -o integral_test integral_test.o integral.a -lm


list_test.o: tests/list_test.c list.h
 gcc -g -c tests/list_test.c -o list_test.o

list_test: list_test.o list.a
 gcc -g -static -o list_test list_test.o list.a 


stack_test.o: tests/stack_test.c stack.h
 gcc -g -c tests/stack_test.c -o stack_test.o

stack_test: stack_test.o stack.a
 gcc -g -static -o stack_test stack_test.o stack.a 


run_tests: equation_test integral_test list_test stack_test
 ./equation_test
 ./integral_test
 ./list_test
 ./stack_test


# -- Сборка бинарников без тестов

integral: integral.o integral.a
 gcc -g -static -o integral integral.o integral.a -lm
 ./integral


equation: equation.o equation.a
 gcc -g -static -o equation equation.o equation.a -lm
 ./equation


list: list.o list.a
 gcc -g -static -o list list.o list.a
 ./list


stack: stack.o stack.a
 gcc -g -static -o stack stack.o stack.a
 ./stack
