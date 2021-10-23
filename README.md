from operator import itemgetter
from typing import List, Tuple, Any


class microprocessor:
    """Микропроцессор"""

    def __init__(self, id, title, sal, comp_id):
        self.id = id
        self.title = title
        self.sal = sal
        self.comp_id = comp_id


class Computer:
    """Компьютер"""

    def __init__(self, id, name):
        self.id = id
        self.name = name


class ComputerMicroprocessor:
    """
    '' для реализации
    связи многие-ко-многим
    """

    def __init__(self, comp_id, mic_id):
        self.comp_id = comp_id
        self.mic_id = mic_id

# Компьютеры
Computers = [
    Computer(1, 'MSI'),
    Computer(2, 'ASUS'),
    Computer(3, 'Lenovo'),
    Computer(4, 'Imac'),
    Computer(5, 'Xiaomi'),
]

# Микропроцессоры
Microprocessors = [
    microprocessor(1, 'AMD A8', 253, 3),
    microprocessor(2, 'AMD Ryzen 5', 222, 2),
    microprocessor(3, 'Intel Core i5', 434, 5),
    microprocessor(4, 'AMD Athlon', 370, 2),
    microprocessor(5, 'Intel Core i7', 556, 3),
]

Microprocessor_Computer = [
    ComputerMicroprocessor(1, 3),
    ComputerMicroprocessor(2, 2),
    ComputerMicroprocessor(3, 5),
    ComputerMicroprocessor(4, 2),
    ComputerMicroprocessor(5, 3),

    ComputerMicroprocessor(1, 2),
    ComputerMicroprocessor(2, 4),
    ComputerMicroprocessor(3, 1),
    ComputerMicroprocessor(4, 4),
    ComputerMicroprocessor(5, 1),
]
def main():
    """Основная функция"""
    # Соединение данных один-ко-многим
one_to_many = [(m.title, m.sal, c.name)
               for c in Computers
               for m in Microprocessors
               if m.comp_id == c.id]

# Соединение данных многие-ко-многим
many_to_many_temp = [(c.name, cm.comp_id, cm.mic_id)
                     for c in Computers
                     for cm in Microprocessor_Computer
                     if c.id == cm.comp_id]

many_to_many = [(c.title, c.sal, Computer_name)
                for Computer_name, Computer_id, microprocessor_id in many_to_many_temp
                for c in Microprocessors if c.id == microprocessor_id]

print('Задание B1:')
res11 = []
for title, _, Computer in one_to_many:
    if title[0] == "A":
        res11.append((title, Computer))
print(res11, "\n")

print('Задание В2')
res12 = [[one_to_many[0][2], one_to_many[0][1]]]
for title, sal, name in one_to_many:
    if name == res12[len(res12)-1][0]:
        if sal < res12[len(res12)-1][1]:

            res12[len(res12)-1][1] = sal
    else:
            res12.append([title, sal])
print(sorted(res12, key=itemgetter(1)), "\n")


print('Задание В3')
res13 = []
for title, sal, Computer in many_to_many:
    res13.append((title, Computer))
# print (res_13)
print(sorted(res13, key=itemgetter(0)), "\n")

if name == '__main__':
    main()
