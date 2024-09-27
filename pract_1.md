# Configuration_Managment

## Задание 1
Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

```
grep '.*' /etc/passwd | cut -d: -f1 | sort
```

![image](https://github.com/user-attachments/assets/52cc1836-a196-4c28-b6bf-cf322198d252)

## Задание 2
Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов.

```
awk '{print $2, $1}' /etc/protocols | sort -nr | head -n 5
```

![image](https://github.com/user-attachments/assets/60f7653f-07b6-4be8-8cdd-7279352446e1)

## Задание 3
Написать программу banner средствами bash для вывода текстов.

```
#!/bin/bash

text=$*
length=${#text}

for i in $(seq 1 $((length + 2))); do
    line+="-"
done

echo "+${line}+"
echo "| ${text} |"
echo "+${line}+"
```

![image](https://github.com/user-attachments/assets/3f39e998-641b-40ca-8a55-f3896a3c7b0e)

## Задание 4
Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

```
#!/bin/bash

file="$1"

id=$(grep -o -E '\b[a-zA-Z]*\b' "$file" | sort -u)
```

```
grep -oE '\b[a-zA-Z_][a-zA-Z0-9_]*\b' hello.c | grep -vE '\b(int|void|return|if|else|for|while|include|stdio)\b' | sort | uniq
```

![image](https://github.com/user-attachments/assets/e39a7713-0612-4a9d-9982-82a493df5a25)


## Задание 5
Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

```
#!/bin/bash

file=$1

chmod 755 "./$file"

sudo cp "$file" /usr/local/bin/
```

![image](https://github.com/user-attachments/assets/1c760c0e-05fc-4254-a20c-e2c1dacaf00b)
![image](https://github.com/user-attachments/assets/6f1e4e06-dc33-475f-b475-b913353974d0)





