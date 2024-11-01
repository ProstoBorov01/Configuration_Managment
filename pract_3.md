![image](https://github.com/user-attachments/assets/49f43598-408d-4d0a-b251-08dd8e4edcaf)## Задача 1

Реализовать на Jsonnet приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

Решение:
```
local all_groups = ["ИКБО-" + std.toString(i) + "-20" for i in std.range(1, 24)];
local groups = ["ИКБО-4-20", "ИКБО-5-20", "ИКБО-5-20", "ИКБО-63-23"];
local names = ["Иванов И.И.", "Петров П.П.", "Сидоров С.С.", "Саввин С.C."];
local ages = [19, 18, 18, 19]; 

local students = [
  {
    age: ages[i],
    group: groups[i],
    name: names[i]
  } 
  for i in std.range(0, std.length(names) - 1)
];

{
    "groups": all_groups,
    "students": students,
    "subject": "Конфигурационное управление"
}
```

![image](https://github.com/user-attachments/assets/8f4e8630-5d9d-473c-9d64-6da000b52f21)

## Задача 2

Реализовать на Dhall приведенный ниже пример в формате JSON. Использовать в реализации свойство программируемости и принцип DRY.

Решение:
```
let Prelude = https://prelude.dhall-lang.org/v20.2.0/package.dhall

let generateGroup = λ(i : Natural) → "ИКБО-" ++ Prelude.Natural.show (i + 1) ++ "-20"

let groups : List Text =
      Prelude.List.generate 24 Text generateGroup

in  { groups = groups,
      students =
      [ { age = 19, group = "ИКБО-4-20", name = "Иванов И.И." }
      , { age = 18, group = "ИКБО-5-20", name = "Петров П.П." }
      , { age = 18, group = "ИКБО-5-20", name = "Сидоров С.С." }
      , { age = 19, group = "ИКБО-63-23", name = "Саввин C.C." }
      ]
    , subject = "Конфигурационное управление"
 }
```

![image](https://github.com/user-attachments/assets/f4762464-92ad-4893-920b-de8f2062cc68)

## Задача 3

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF.

Язык нулей и единиц.

Решение:
BNF = '''
E = Digit | E Digit
Digit = 0 | 1
'''

![image](https://github.com/user-attachments/assets/1104d035-1755-4e9b-b48a-277fe16949cd)

## Задача 4

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF.

Язык правильно расставленных скобок двух видов.

Решение:
```
BNF = '''
E = "()" | "{}" | E E | "(" E ")" | "{" E "}"
'''
```

![image](https://github.com/user-attachments/assets/8df4ee12-95d8-4c92-84ad-74c18af3638e)

## Задача 5

Реализовать грамматики, описывающие следующие языки (для каждого решения привести БНФ). Код решения должен содержаться в переменной BNF.

Язык выражений алгебры логики.

BNF = '''
E = T EPrime
EPrime = Op T EPrime | 
T = ~ T | ( E ) | Var
Op = & | |
Var = x | y
'''
![image](https://github.com/user-attachments/assets/d8aa6822-12f1-41f7-a483-1159f7b57503)
