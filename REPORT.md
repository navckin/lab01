## Laboratory work I

Данная лабораторная работа посвещена изучению утилит для разработки проектов

## Tasks

- [ ] 1. Ознакомиться со ссылками учебного материала
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Homework

1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.

2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0` 

```bash
tar -xvzf boost_1_69_0.tar.gz -C /home/anya/boost_1_69_0
```
3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.

```bash
Answer: 12;
Command: find ./ -maxdepth 1 -type f | wc -l
```
4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.

```sh
Answer: 61192;
Command: find ./ -type f | wc -l
```
5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```sh
Answer for .h (the headers): 296; Command for .h: find ./ -type f -name "*.h" | wc -l
Answer for .cpp: 13774; Command: find ./ -type f -name "*.cpp" | wc -l
Answer for other files: 47122; Command: find ./ -type f \( ! -name "*.cpp" ! -name "*.h" \) | wc -l
```
6. Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.

```sh
/home/anya/boost_1_69_0/boost_1_69_0/boost/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/proto/detail/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/type_erasure/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/hana/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/hana/fwd/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/fusion/include/any.hpp
/home/anya/boost_1_69_0/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
Command:
find "$(cd ..; pwd)" -name "any.hpp"
```
7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.

```sh
Command: grep -rnw ./ -e boost::asio
A small part of an otput for example:

/boost/process/async_pipe.hpp:200:    handle_type sink  (::boost::asio::io_context& ios) const &;
./boost/process/io.hpp:94:boost::asio::io_context ios;
./boost/process/io.hpp:126:template<typename T> using is_streambuf    = typename std::is_same<T, boost::asio::streambuf>::type;
./boost/process/io.hpp:129:            std::is_same<   boost::asio::const_buffer, T>::value |
./boost/process/io.hpp:130:            std::is_base_of<boost::asio::const_buffer, T>::value
./boost/process/io.hpp:134:            std::is_same<   boost::asio::mutable_buffer, T>::value |

```
8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).

```sh
Возникла проблема при компилировании. При вызове команды ./bootstrap.sh --prefix=boost_output не было права доступа. Исправление такой проблемы находится по ссылке : https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/
Последовательность комнад для устранения пробелмы:
1). sudo apt update обновляемся. (updating the packages list)
2). sudo apt install build-essential устанавливаем build-essential package. Эта команда устанавлиает много "пакетов", включая необходимый нам для работы gcc (Install the build-essential package, The command installs a bunch of new packages including gcc, g++ and make.)
3). gcc --version Производим проверку (удачно ли установилось). Там должна вернуться версия GCC (To validate that the GCC compiler is successfully installed, use the gcc --version command which prints the GCC version)
4). ./bootstrap.sh --prefix=boost_output --with-toolset=gcc Вызываем необходимую нам комнаду при помощи "инструмента" gcc.
5) ./b2 install Компилируем (build) boost
```
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.

```sh
1). Для этого созадем папку boost-libs. Используем команду: mkdir -p ./boost-libs
 2) При помощи команды mv меняем расположение статических библиотек 
 mv /home/anya/boost_1_69_0/boost_output/include /home/anya/boost-libs 
 mv /home/anya/boost_1_69_0/boost_output/lib /home/anya/boost-libs
```
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.

```sh
Answer ( a small part of the whole output) 
20K	./include/boost/wave/util/cpp_macromap_utils.hpp
4,0K	./include/boost/wave/util/symbol_table.hpp
96K	./include/boost/wave/util/cpp_iterator.hpp
8,0K	./include/boost/wave/util/macro_definition.hpp
8,0K	./include/boost/wave/util/functor_input.hpp
8,0K	./include/boost/wave/util/time_conversion_helper.hpp
72K	./include/boost/wave/util/flex_string.hpp
8,0K	./include/boost/wave/util/file_position.hpp
8,0K	./include/boost/wave/util/cpp_ifblock.hpp
Command: du -a -h
```
11. Найдите *топ10* самых "тяжёлых".

```sh
Output:
54M	./lib
5,3M	./include/boost/fusion/container/generation/detail/preprocessed
5,1M	./include/boost/phoenix/statement/detail/preprocessed
4,5M	./include/boost/typeof
4,5M	./include/boost/phoenix/core/detail/cpp03/preprocessed
3,8M	./include/boost/geometry/srs/projections
2,7M	./include/boost/fusion/container/vector/detail/cpp03/preprocessed
2,0M	./include/boost/qvm/gen
2,0M	./include/boost/phoenix/scope/detail/cpp03/preprocessed
2,0M	./include/boost/numeric/ublas
Command: du -Sh | sort -rh | head -10
```



```
Copyright (c) 2015-2020 The ISC Authors
```
