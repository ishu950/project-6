# project-6
snake game


from turtle import Screen
from questionmodel import Snake
from food import Food
import time
from scoreboard import Scoreboard
screen = Screen()
screen.setup(width=600, height=600)
screen.bgcolor("black")
screen.title("my snake game")
screen.tracer(0)

snake = Snake()
food = Food()
scoreboard = Scoreboard()
screen.listen()

screen.onkey(snake.up, "U")
screen.onkey(snake.down, "D")
screen.onkey(snake.left, "L")
screen.onkey(snake.right, "R")
game_is_on = True
while game_is_on:
    screen.update()
    time.sleep(0.1)
    snake.move()

    if snake.head.distance(food) < 15:
        food.refresh()
        snake.extend()
        scoreboard.increase_score()

    for seg in snake.segment[1:]:
        if snake.head.distance(seg) < 10 :
            game_is_on=False
            scoreboard.game_over()




    if snake.head.xcor() > 280 or snake.head.xcor()  < -280 or snake.head.ycor() > 280 or snake.head.ycor() < -280:
        game_is_on=False
        scoreboard.game_over()


screen.exitonclick()
