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



Перед отправкой решения проверьте его в ShellCheck на предупреждения.

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

![image](https://github.com/user-attachments/assets/a1a7d512-826b-4a32-8571-7d983666e98a)


## Задание 5
Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

```
#!/bin/bash

file=$1

chmod 755 "./$file"

sudo cp "$file" /usr/local/bin/
```


