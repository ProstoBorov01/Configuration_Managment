## Задача 1

Написать программу на Питоне, которая транслирует граф зависимостей civgraph в makefile в духе примера выше. Для мало знакомых с Питоном используется упрощенный вариант civgraph: [civgraph.json](civgraph.json).

## Решение:

```Python
import json


def parse_civgraph(civgraph_file):

    with open(civgraph_file, 'r') as file: data = json.load(file)

    return data


def generate_makefile(data, output_file):

    with open(output_file, 'w') as file:

        for target, dependencies in data.items():
           
            dep_str = " ".join(dependencies) if dependencies else ""
            file.write(f"{target}: {dep_str}\n")
            file.write(f"\t@echo {target}\n\n") 


def main():

    civgraph_file = "civgraph.json"  
    output_file = "Makefile"  
    data = parse_civgraph(civgraph_file)

    generate_makefile(data, output_file)
    print(f"Makefile был сгенерирован в {output_file}")


if __name__ == "__main__": main()
```

![image](https://github.com/user-attachments/assets/afe40e92-0ca4-4b4c-bb75-e07f73e7a613)
