import pygame
import time
import random

pygame.init()

# Определение цветов
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)

dis_width = 800
dis_height = 600
dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('Змейка')

clock = pygame.time.Clock()

snake_block = 10
snake_speed = 15

font_style = pygame.font.SysFont(None, 50)


def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 6, dis_height / 3])


def gameLoop():
    game_over = False
    game_close = False

    x1 = dis_width / 2
    y1 = dis_height / 2

    x1_change = 0
    y1_change = 0

    snake_List = []
    Length_of_snake = 1

    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0

    while not game_over:

        while game_close == True:
            dis.fill(blue)
            message("Вы проиграли! Нажмите Q-выход или C-снова", red)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0

        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += x1_change
        y1 += y1_change
        dis.fill(blue)
        pygame.draw.rect(dis, green, [foodx, foody, snake_block, snake_block])

        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]

        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True

        for x in snake_List:
            pygame.draw.rect(dis, black, [x[0], x[1], snake_block, snake_block])

        pygame.display.update()

        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
            foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
            Length_of_snake += 1

        clock.tick(snake_speed)

    pygame.quit()
    quit()


gameLoop()# snake.py
Snake.py

Этот код представляет собой простую реализацию игры "Змейка" на языке программирования Python с использованием библиотеки Pygame. Вот пошаговое объяснение того, что делает этот код:
1. Импортируются необходимые библиотеки: pygame, time и random.
2. Определяются цвета в формате RGB.
3. Устанавливается размер окна для отображения игры.
4. Создается окно с заголовком "Змейка".
5. Инициализируется часы для управления скоростью игры.
6. Задаются параметры для размера блока змейки и скорости змейки.
7. Определяется стиль шрифта для вывода сообщений.
8. Создается функция message, которая отображает сообщение на экране.
9. Определяется функция gameLoop, которая содержит основную логику игры.
10. Игра начинается с создания змейки и случайного расположения еды на поле.
11. В основном цикле игры проверяются действия пользователя (нажатия клавиш) и обновляется состояние игры в соответствии с этими действиями.
12. Если змейка выходит за границы поля или сталкивается сама с собой, игра завершается.
13. Если змейка съедает еду, еда перемещается на новое случайное место, а длина змейки увеличивается.
14. Игра продолжается до тех пор, пока игрок не проиграет или не завершит игру.
15. После завершения игры окно закрывается.
Результатом выполнения этого кода будет запуск игры "Змейка" в окне Pygame, где игрок будет управлять змейкой, собирать еду и стараться не столкнуться со стенами или самим собой.
