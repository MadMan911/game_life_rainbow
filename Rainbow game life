import pygame as p
from pygame.locals import *
import random
import time


# подсчет соседей
def near(cells, i, j):
    # границ нет, то есть идешь вправо -> появляешься слева
    count = 0
    for y in range(-1, 2):
        for x in range(-1, 2):
            if cells[(i + y) % len(cells)][(j + x) % len(cells[0])] == 1:
                count += 1
    if cells[i][j] == 1:
        count -= 1
    return count
    # есть границы
    # count = 0
    # for y in range(-1, 2):
    #     for x in range(-1, 2):
    #         if 0 <= x <=len(cells[0])  and 0 <= y <= len(cells) and cells[(i + x) % len(cells[0])][(j + y) % len(cells[0])] == 1 and x != i and y != j:
    #             count += 1
    # return count


# константы цветов
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
# размер квадратов(клеток)
a = 20
# создаем поле
w = 600
h = 600
root = p.display.set_mode((w, h))
# заполняем поле
cells = []
for i in range(0, root.get_height() // a):
    cells.append([])
    for j in range(0, root.get_width() // a):
        cells[i].append(random.choice([0, 0, 1]))

# основная логика
k = 0
while True:
    time.sleep(0.1)
    # красим экранн в белый
    root.fill(WHITE)
    # рисуем сетку
    ## for i in range(0, root.get_height() // a):
    ##     p.draw.line(root, BLACK, (0, i * a), (root.get_width(), i * a))
    ## for j in range(0, root.get_width() // a):
    ##     p.draw.line(root, BLACK, (j * a, 0), (j * a, root.get_height()))
    ## чтобы при закрытии шинвоудс не думал, что прога не отвечает
    for i in p.event.get():
        if i.type == QUIT:
            quit()
    # проходимся по всем клеткам и раскрашиваем
    # k = 0
    for i in range(0, len(cells)):
        for j in range(0, len(cells[0])):
            print(cells[i][j], i, j)
            if cells[i][j] == 0:
                p.draw.rect(root, BLACK, [i * a, j * a, a, a])
            else:
                k += 10
                p.draw.rect(root, (k * 100 * i % 256, (k + 200 * i * j) % 256, k * k * 122 * j % 256),
                            [i * a, j * a, a, a])  # (100*i%256,200*i*j%256,122*j%256)
    # обновляем эkран
    p.display.update()

    # оcновная логика с умиранием и возрождением клеток
    cells2 = [[0 for j in range(len(cells[0]))] for i in range(len(cells))]
    for i in range(len(cells)):
        for j in range(len(cells[0])):
            if cells[i][j] == 1:
                if near(cells, i, j) not in [2, 3]:
                    # if near( [i ,j]) not in [2,3]:
                    cells2[i][j] = 0
                    continue
                else:
                    cells2[i][j] = 1

            else:
                if near(cells, i, j) in [3]:
                    # if near([i,j]) in [3]:
                    cells2[i][j] = 1
                else:
                    cells2[i][j] = 0

    for i in range(len(cells2)):
        for j in range(len(cells2[i])):
            cells[i][j] = cells2[i][j]
