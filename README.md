Вариант №24<br/>
Задание №3<br/>
Разработать инструмент командной строки для учебного конфигурационного
языка, синтаксис которого приведен далее. Этот инструмент преобразует текст из
входного формата в выходной. Синтаксические ошибки выявляются с выдачей
сообщений.
Входной текст на учебном конфигурационном языке принимается из
файла, путь к которому задан ключом командной строки. Выходной текст на
языке yaml попадает в файл, путь к которому задан ключом командной строки.
Массивы:
( значение, значение, значение, ... )
Словари:
@{
 имя = значение;
 имя = значение;
 имя = значение;
 ...
}
Имена:
[_A-Z][_a-zA-Z0-9]*
Значения:
• Числа.
• Строки.
• Массивы.
• Словари.
Строки:
"Это строка"
Объявление константы на этапе трансляции:
var имя = значение
Вычисление константы на этапе трансляции:
^[имя]
Результатом вычисления константного выражения является значение.
Все конструкции учебного конфигурационного языка (с учетом их возможной вложенности) должны быть покрыты тестами. Необходимо показать 2
примера описания конфигураций из разных предметных областей.

Описание функций<br/>
1. rtokenize(self)<br/>
Назначение:<br/>
УРазбивает входной текст на список токенов в соответствии с заданными правилами.<br/>

Параметры:  <br/>
Нет. Использует текст, переданный при инициализации класса Lexer.<br/>

Возвращает: <br/>
Ничего не возвращает. Обновляет атрибут self.tokens объекта.<br/>


3. peek(self)<br/>
Назначение: Возвращает текущий токен, не удаляя его из очереди.<br/>
Параметры:нет.<br/>
Возвращает: Текущий токен (tuple) или None, если токены закончились.<br/>

4. next_token(self)<br/>
Назначение: Извлекает и возвращает текущий токен из списка токенов.<br/>
Параметры: нет.<br/>
Возвращает: Извлечённый токен (tuple) или None, если токены закончились.<br/>

5. parse(self)<br/>
Назначение: Обрабатывает список токенов и возвращает результат разбора.<br/>
Параметры: нет.<br/>
Возвращает: Объект Python, представляющий разобранные данные (список или словарь).<br/>

6.statement(self)<br/>
Назначение: Определяет тип следующей конструкции (переменная, массив или словарь) и обрабатывает её.<br/>
Параметры: Нет.<br/>
Возвращает:  Результат разбора конструкции (например, переменной, массива или словаря).<br/>

7.parse_var(self)<br/>
Назначение: Разбирает объявление переменной и сохраняет её значение.<br/>
Параметры: Нет.<br/>
Возвращает:  Словарь, где ключ — имя переменной, а значение — её значение.<br/>

8.parse_value(self)<br/>
Назначение: Обрабатывает и возвращает значение, заданное в текущей конструкции.<br/>
Параметры: Нет.<br/>
Возвращает:  Значение (число, строка, массив, словарь, булево или вычисление). <br/>

9.parse_array(self)<br/>
Назначение:Разбирает массив и возвращает его элементы.<br/>
Параметры: Нет.<br/>
Возвращает: Список, содержащий элементы массива.<br/>

10.parse_dict(self)<br/>
Назначение:Разбирает словарь и возвращает его ключи и значения.<br/>
Параметры: Нет.<br/>
Возвращает: Словарь, содержащий пары ключ-значение.<br/>

11.parse_eval(self)<br/>
Назначение:Обрабатывает выражения с вычислением значений, поддерживает базовые арифметические операции.<br/>
Параметры: Нет.<br/>
Возвращает: Результат вычисления (число).<br/>

12.expect(self, token_type)<br/>
Назначение:Проверяет, соответствует ли текущий токен ожидаемому типу, и переходит к следующему токену.<br/>
Параметры: token_type (str): Ожидаемый тип токена.<br/>
Возвращает: Ничего не возвращает. Генерирует ошибку, если токен не соответствует.<br/>

12.convert_to_yaml(data)<br/>
Назначение:Конвертирует объект Python в строку YAML-формата.<br/>
Параметры: data (Any): Объект для конвертации.<br/>
Возвращает: Строку в формате YAML.<br/>

***
НАСТРОЙКИ<br/>
input.txt
var days_in_week = 7<br/>

var schedule = @{<br/>
    monday = @{<br/>
        subject = "Mathematics"<br/>
        teacher = "Prof. Smith"<br/>
        time = "9:00"<br/>
    };<br/>
    tuesday = @{<br/>
        subject = "Physics"<br/>
        teacher = "Dr. Brown"<br/>
        time = "10:00"<br/>
    };<br/>
    wednesday = @{<br/>
        subject = "Literature"<br/>
        teacher = "Mrs. Johnson"<br/>
        time = "11:00"<br/>
    };<br/>
    thursday = @{<br/>
        subject = "Chemistry"<br/>
        teacher = "Dr. Green"<br/>
        time = "14:00"<br/>
    };<br/>
    friday = @{<br/>
        subject = "Computer Science"<br/>
        teacher = "Prof. Black"<br/>
        time = "15:00"<br/>
    };<br/>
}<br/>

var total_classes = ^days_in_week * 5<br/>

var class_schedule = @{<br/>
    week = ^total_classes<br/>
}<br/>

input_m.txt<br/>
var total_tasks = 20<br/>
var completed_tasks = 8<br/>

var project = @{<br/>
    project_name = "Web Development"<br/>
    duration_weeks = 12<br/>
    team = (<br/>
        "Alice",<br/>
        "Bob",<br/>
        "Charlie"<br/>
    )<br/>
    tasks = (<br/>
        "Design homepage",<br/>
        "Implement login system",<br/>
        "Create database schema",<br/>
        "Develop user authentication",<br/>
        "Write unit tests"<br/>
    )<br/>
}<br/>

var progress = ^completed_tasks / ^total_tasks * 100<br/>

var team_progress = @{<br/>
    progress = ^progress<br/>
}<br/>

ТЕСТЫ для INPUT.TXT<br/>
![image](https://github.com/user-attachments/assets/7fa5d891-ea7f-41d6-9ad8-239d4dc1848f)<br/>
ТЕСТЫ для INPUT_M.TXT<br/>
![image](https://github.com/user-attachments/assets/4fcd154a-75e9-4a72-bc06-a320066d02b8)<br/>






