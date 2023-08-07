# **Bookypedia**

Bookypedia — консольная программа, которая позволяет хранить информацию о книгах в БД Postgres. В программе реализована поддержка трех таблиц: Авторы, Книги, Теги. В качестве SQL-клиента используется библиотека libpqxx. Манипулирование данными происходит с помощью предопределенных команд.

## **Команды**

1. ***AddAuthor***

Команда `AddAuthor <name>` добавляет в БД автора книги с указанным именем. Пример:
```
AddAuthor Joanne Rowling
AddAuthor Antoine de Saint-Exupery
```

2. ***ShowAuthors***

Команда `ShowAuthors` позволяет вывести нумерованный список авторов, отсортированный по алфавиту. Пример:

```
AddAuthor Joanne Rowling
AddAuthor Jack London
ShowAuthors
1. Jack London
2. Joanne Rowling 
```

3. ***DeleteAuthor***

Команда `DeleteAuthor <name> or empty` Удаляет выбранного автора, все его книги и связанные с этими книгами теги. Пример:
```
DeleteAuthor
1 Jack London
2 Joanne Rowling
Enter author # or empty line to cancel
1
ShowAuthors
1 Joanne Rowling 
```

```
ShowAuthors
1 Jack London
2 Joanne Rowling
DeleteAuthor Jack London
ShowAuthors
1 Joanne Rowling 
```

4. ***EditAuthor***

Команда `EditAuthor <name> or empty` позволяет редактировать указанного автора. Пример:
```
EditAuthor
1 Jack London
2 Joanne Rowling
Enter author # or empty line to cancel
2
Enter new name:
J. K. Rowling
EditAuthor Jack London
Enter new name:
John Griffith Chaney
ShowAuthors
1 J. K. Rowling
2 John Griffith Chaney
```

5. ***AddBook***

Команда `AddBook <pub_year> <title>` добавляет в БД книгу с указанным названием и годом публикации. Пример:
```
AddBook 1906 White Fang
Enter author name or empty line to select from list:
Jack London
No author found. Do you want to add Jack London (y/n)?
y
Enter tags (comma separated):
adventure, dog, gold rush, dogs 
```

6. ***ShowBooks***

Команда `ShowBooks` позволяет вывести нумерованный список книг, отсортированный по названию, по имени автора, по возрастанию года публикации. Пример:
```
ShowBooks
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fang by Jack London, 1906 
```

7. ***ShowAuthorBooks***

Команда `ShowAuthorBooks` выводит нумерованный список книг выбранного автора с годами их выпуска, отсортированный по году публикации и по названию. Пример:

```
ShowAuthorBooks
Select author:
1 Boris Akunin
2 Jack London
3 Joanne Rowling
4 Herman Melville
Enter author # or empty line to cancel
1
1 Azazelle, 1998
2 Murder on the Leviathan, 1998
3 The Turkish Gambit, 1998
4 She Lover of Death, 200
```

8. ***ShowBook***

Команда `ShowBook <title> or empty` выводит подробную информацию о книге: автор, название, год публикации, теги, если есть. Пример:
```
ShowBooks
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fang by Jack London, 1906
ShowBook White Fang
Title: White Fang
Author: Jack London
Publication year: 1906
Tags: adventure, dog, gold rush
ShowBook The Cloud Atlas
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
Enter the book # or empty line to cancel:
2
Title: The Cloud Atlas
Author: Liam Callanan
Publication year: 2004
ShowBook
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fang by Jack London, 1906
Enter the book # or empty line to cancel:
3
Title: White Fang
Author: Jack London
Publication year: 1906
Tags: adventure, dog, gold rush
```

9. ***DeleteBook***

Команда `DeleteBook <title> or empty` позволяет удалить книгу, указав её название напрямую или выбрав из списка. Пример:
```
ShowBooks
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fang by Jack London, 1906
DeleteBook The Cloud Atlas
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
Enter the book # or empty line to cancel:
2
ShowBooks
1 The Cloud Atlas by David Mitchell, 2004
2 White Fang by Jack London, 1906
DeleteBook
1 The Cloud Atlas by David Mitchell, 2004
2 White Fang by Jack London, 1906
Enter the book # or empty line to cancel:
1
```

10. ***EditBook***

Команда `EditBook <title> or empty` позволяет отредактировать книгу, указав её название напрямую или выбрав из списка. Пример:
```
ShowBooks
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fan by Jack London, 1906
EditBook White Fan
Enter new title or empty line to use the current one (White Fan):
White Fang
Enter publication year or empty line to use the current one (1906):

Enter tags (current tags: adventure, cat, gold rush):
adventure, gold rush, dog
ShowBook White Fang
Title: White Fang
Author: Jack London
Publication year: 1096
Tags: adventure, dog, gold rush
EditBook
1 The Cloud Atlas by David Mitchell, 2004
2 The Cloud Atlas by Liam Callanan, 2004
3 White Fang by Jack London, 1906
Enter the book # or empty line to cancel:
3
Enter new title or empty line to use the current one (White Fang):

Enter publication year or empty line to use the current one (1906):

Enter tags (current tags: adventure, dog, gold rush):
adventure, gold rush, dog, wolf
```

## **Запуск**
При запуске программа должна считать URL базы данных из переменной окружения BOOKYPEDIA_DB_URL.
```bash
export BOOKYPEDIA_DB_URL=postgres://user:password@localhost:30432/bookypedia_db
```

## **Зависимости**
1. [С++20](https://en.cppreference.com/w/cpp/20)
2. [PostgreSQL](https://www.postgresql.org/) 15+ version requires
3. [libpqxx](https://github.com/jtv/libpqxx)
4. [Boost](https://www.boost.org/users/history/version_1_78_0.html) 1.78+ version requires
5. [GCC](https://gcc.gnu.org/) 11+ version requires
6. [CMake](https://cmake.org) 3.11 version requires
7. [Conan](https://conan.io/) 1.* version reqires