def welcome():
    print(' Приветствую, игроки! ')
    print(' Сейчас Вы сможете сразиться в игре ')
    print('                "Крестики-нолики" ')
    print(' Укажите два числа. X - номер строки и Y - номер столбца. ')
def show():
    print()
    print('     |  0  |  1  |  2  | ')
    print(' ------------------ ')
    for i, row in enumerate(field):
        row_str = f' {i} | {'  |  ' .join(row)} | '
        print(row_str)
        print(' ------------------')
    print()
def ask():
    while True:
        cords = input('            Ваш ход: ').split()
        if len(cords) != 2:
            print(' Введите 2 координаты! ')
            continue
        x, y = cords
        if not (x.isdigit()) or not (y.isdigit()):
            print(' Введите числа !')
            continue
        x, y = int(x), int(y)
        if 0 > x or x > 2 or 0 > y or y > 2:
            print(' Координаты вне диапазона! ')
            continue
        if field[x][y] != '   ':
            print(' Клетка занята!')
            continue
        return x, y
def check_win():
    win_cord = [((0, 0), (0, 1), (0, 2)), ((1, 0), (1, 1), (1, 2)), ((2, 0), (2, 1), (2, 2)), ((0, 2), (1, 1), (2, 0)), ((0, 0), (1, 1), (2, 2)), ((0, 0), (1, 0), (2, 0)), ((0, 1), (1, 1), (2, 1)), ((0, 2), (1, 2), (2, 2))]
    for cord in win_cord:
        a = cord[0]
        b = cord[1]
        c = cord[2]
        if field[a[0]][a[1]] == field[b[0]][b[1]] == field[c[0]][c[1]] != '   ':
            print(f' Выиграл {field[a[0]][a[1]]}!')
            return True
    return False

welcome()
field = [['   '] * 3 for i in range(3)]
num = 0
while True:
    num += 1
    show()
    if num % 2 == 1:
        print(' Ходит крестик! ')
    else:
        print(' Ходит нолик! ')
    x, y = ask()
    if num % 2 == 1:
        field[x][y] = 'X'
    else:
        field[x][y] = '0'
    if check_win():
        break
    if num == 9:
        print(' Ничья! ')
        break
