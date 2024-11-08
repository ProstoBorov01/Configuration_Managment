## Задание 1

```
Enter git commands below.
git commit
git branch fitst
git commit
git commit
git checkout first
Cannot find commit: first
git checkout fitst
git commit
git commit
git checkout master
git merge first
Cannot find ref: first
git merge fift
Cannot find ref: fift
git merge fifst
Cannot find ref: fifst
git merge fitst
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
git checkout -b second
git commit
git commit
git rebase master
git rebase second
Already up-to-date.
git checkout master
git rebase second
Fast-forwarded to second.
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
git checkout HEAD^
```
![alt text](image.png)

## Задание 2

```
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git init
Initialized empty Git repository in C:/Users/SavvinPC/Documents/МИРЭА/Конфигурационное управление/pract/pract_4/.git/
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git config --global user.name "coder1"
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git config --global user.email "coder1@something.com"
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git add .
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git commit -m "init"                
[master (root-commit) a87d3ea] init
 3 files changed, 45 insertions(+)
 create mode 100644 image.png
 create mode 100644 pract.md
 create mode 100644 prog.py
PS C:\Users\SavvinPC\Documents\МИРЭА\Конфигурационное управление\pract\pract_4> git log
commit a87d3ea48023e832acaf5df754fa3918389d19c1 (HEAD -> master)
Author: coder1 <coder1@something.com>
Date:   Fri Nov 6 16:50:02 2024 +0300

    init
```

## Задание 3

```
# 1. Создание bare-репозитория
git init --bare ../server

# 2. Добавление remote и пуш
git remote add server ../server
git push server --all
git remote -v

# 3. Синхронизация coder1
git fetch server
git pull server master

# 4. Клонирование для coder2
git clone server coder2

# 5. Настройка coder2
git config user.name "coder2"
git config user.email "coder2@corp.com"

# 6. Добавление readme.md
git add readme.md
git commit -m "Добавить readme.md с описанием программы"
git push origin master

# 7. Coder1 получает обновления
git pull server master

# 8. Coder1 добавляет свою информацию
git add readme.md
git commit -m "Добавить информацию об авторе: coder1"
git push server master

# 9. Coder2 добавляет свою информацию и решает конфликты
git pull origin master
# (разрешение конфликтов в readme.md)
git add readme.md
git commit -m "Разрешить конфликт и добавить информацию об авторе: coder2"
git push origin master

# 10. Просмотр git log
git log 

Вывод:

commit 342636f0e78ee0b7b05dd3596a615112e8de0706 (HEAD -> master, origin/master, origin/HEAD)
Author: coder2 <coder2@corp.com>
Date:   Thu Nov 8 13:33:05 2024 +0300

    Добавить readme.md с описанием программы

commit 6bf5414fc8c660b10269fd865b0ce80f3314f075
Author: coder1 <coder1@something.com>
Date:   Thu Nov 7 22:32:52 2024 +0300

    Добавить информацию об авторе: coder1

commit 344970ffc83db44f86e0f25eb34527428146ef3f
Author: coder2 <coder2@corp.com>
Date:   Wed Oct 30 16:45:02 2024 +0300

    Разрешить конфликт и добавить информацию об авторе: coder2

commit a4bc2b302dd3e90e956b8c5b4e96b00bf3cda52b
Author: coder1 <coder1@something.com>
Date:   Mon Oct 28 19:34:28 2024 +0300

    Добавлен основной файл программы prog.py

```

## Задание 4

```
import subprocess
from concurrent.futures import ThreadPoolExecutor, as_completed

def get_git_objects():
    try:
        result = subprocess.run(
            ["git", "rev-list", "--all", "--objects"],
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True,
            check=True
        )
    except subprocess.CalledProcessError as e:
        print(f"Ошибка при выполнении git rev-list: {e.stderr}")
        return []

    objects = set()
    for line in result.stdout.strip().splitlines():
        parts = line.split()
        if parts:
            objects.add(parts[0])

    return list(objects)

def display_object_content(object_id):
    try:
        result = subprocess.run(
            ["git", "cat-file", "-p", object_id],
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True,
            check=True
        )
        return f"Object ID: {object_id}\n{result.stdout}\n{'=' * 40}\n"
    except subprocess.CalledProcessError as e:
        return f"Ошибка при выполнении git cat-file для объекта {object_id}: {e.stderr}\n"

def main():
    objects = get_git_objects()
    if not objects:
        print("Нет объектов для отображения.")
        return

    print(f"Найдено {len(objects)} уникальных объектов.\n")

    with ThreadPoolExecutor(max_workers=10) as executor:
        future_to_object = {executor.submit(display_object_content, obj): obj for obj in objects}
        for future in as_completed(future_to_object):
            output = future.result()
            print(output)

if __name__ == "__main__":
    main()
```
