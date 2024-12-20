Реализовать с помощью математического языка LaTeX нижеприведенную формулу:

![image](https://github.com/user-attachments/assets/4a986823-dfe7-45f2-8900-f68dbc259843)

Прислать код на LaTeX и картинку-результат, где, помимо формулы, будет указано ФИО студента.

## Решение

```LaTeX
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage[russian]{babel}
\usepackage{amsmath}
\usepackage[T2A]{fontenc}
\begin{document}


\[
\int_{x}^{\infty} \frac{dt}{t(t^2 - 1) \log t} = \int_{x}^{\infty} \frac{1}{t \log t} \left( \sum_{m=1}^{\infty} t^{-2m} \right) dt = \sum_{m=1}^{\infty} \int_{x}^{\infty} \frac{t^{-2m}}{t \log t} dt = \sum_{m=1}^{\infty} \operatorname{li}(x^{-2m})
\]

\end{document}
```

## Результат

![image](https://github.com/user-attachments/assets/c50fd8ae-e5dc-4d83-ab37-c0d5f829843d)

## Задача 2

На языке PlantUML реализовать диаграмму на рисунке ниже. Прислать текст на PlantUML и картинку-результат, в которой ФИО студента заменены Вашими собственными.
Обратите внимание на оформление, желательно придерживаться именно его, то есть без стандартного желтого цвета и проч. Чтобы много не писать используйте псевдонимы с помощью ключевого слова "as".

## Решение

```PlantUML
@startuml
skinparam lifelineStrategy nosolid
actor "Студент Саввин Сергей" as S
database Piazza as P
actor Преподаватель as T

T -> P : Публикация задачи
activate P
P --> T : Задача опубликована
deactivate P
...
S -> P : Поиск задач
activate P
P --> S : Получение задачи
deactivate P
...
S -> P : Публикация решения
activate P
P --> S : Решение опубликовано
deactivate P
...
T -> P : Поиск решений
activate P
P --> T : Решение найдено
T -> P : Публикация оценки
P --> T : Оценка опубликована
deactivate P
...
S -> P : Проверка оценки
activate P
P --> S : Оценка получена
deactivate P
@enduml
```

## Результат

![image](https://github.com/user-attachments/assets/245a729d-aa47-4bd9-a948-61940d3d0dc6)

