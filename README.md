# linuxhelp

 - process tree: `ps -ef --forest`
 - list processes in info of which presented word `gdbserver`: `ps -ef |grep gdbserver`
 - kill process with id(`pid` must be actual identifier of process): `kill -9 pid`
 - print strings contained in a binary: `strings /path/to/binary`
 - list dynamic libraries on which our binary is dependant(for linux): `ldd -v /path/to/binary`
 - list dynamic libraries on which our binary is dependant(for macos): `ldd-apple.sh /path/to/binary`
 - find string in a binary: `strings -t d -f -n 24 /path/to/binary | grep -i "string content"`

Проверка того прилинкована ли статическая библиотека libboost_stacktrace_addr2line.a к бинарнику utils_simple_resource_tests(работает только если и там и там присутствует отладочная информация)
1. сохраняем информацию о символах в файлы:
  `nm $HOME/installed/boost/Debug/lib/libboost_stacktrace_addr2line.a > st_a2l.txt`
  `nm $HOME/builds/utils/xcode/tests/Debug/utils_simple_resource_tests > simple.txt`
2. сравниваем результат. Если есть одинаковые строки(с поправкой на адрес), то вероятнее всего что статическая библиотека
   libboost_stacktrace_addr2line.a была прилинкована к файлу utils_simple_resource_tests. Также надо иметь ввиду что линкер поместит из библиотеки
   libboost_stacktrace_addr2line.a не все символы, а лишь те в которых нуждается utils_simple_resource_tests.
