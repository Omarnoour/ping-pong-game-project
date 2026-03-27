# ping-pong-game-project
 
import turtle
#setup window=============
window = turtle.Screen()
window.title("ping Pong by omar")
window.setup(width=800, height=600)
window.tracer(0)
window.bgcolor(.1,.1,.1)

#setup game objects
#the ball
ball= turtle.Turtle()
ball.speed(0)
ball.shape("square")
ball.color("white")
ball.shapesize(stretch_len=1, stretch_wid=1)
ball.goto(x=0,y=0)
ball.penup()
ball_dx , ball_dy = 1 , 1
ball_speed = .4

#make ceter line
center_line = turtle.Turtle()
center_line.speed(0)
center_line.shape("square")
center_line.color("white")
#to get wid = 500px =25 * 20 px desfult
center_line.shapesize(stretch_len=.1 , stretch_wid=25)
center_line.goto(x=0 , y=0)
center_line.penup()

#player 1
player1 = turtle.Turtle()
player1.speed(0)
player1.shape("square")
player1.color("red")
player1.shapesize(stretch_len=1, stretch_wid=5)
player1.penup()
player1.goto(x=-360,y=0 )

#PLAYER2
player2= turtle.Turtle()
player2.speed(0)
player2.shape("square")
player2.color("blue")
player2.shapesize(stretch_len=1, stretch_wid=5)
player2.penup()
player2.goto(x= 360, y=0)

#score board

score = turtle.Turtle()
score.speed(0)
score.color("white")
score.penup()
score.goto(x=0,y=260)
score.write("player1: 0 player2: 0", align="center" ,
            font=("courier", 14 , "normal") )
score.hideturtle()    #to see the text only =====
p1_score, p2_score = 0 , 0

#players movment === recive inputs from user for moving

players_speed = 20

def p1_move_up():
    player1.sety(player1.ycor() + players_speed)
def p1_move_down():
    player1.sety(player1.ycor() -players_speed)

def p2_move_up():
    player2.sety(player2.ycor() + players_speed)
def p2_move_down():
    player2.sety(player2.ycor() - players_speed)

#the control sysytem

window.listen()
window.onkeypress(p1_move_up, "w")
window.onkeypress(p1_move_down, "s")
window.onkeypress(p2_move_up ,"Up")
window.onkeypress(p2_move_down , "Down")

#ball motion =======





#game loop
while True:
    window.update()

#ball movemnet

    ball.setx(ball.xcor() + (ball_dx * ball_speed))
    ball.sety(ball.ycor() + (ball_dy * ball_speed))

    #ball and boundry of the window
    if(ball.ycor() > 290):
        ball.sety(290)
        ball_dy *= -1  #invert y dirction

    if(ball.ycor() < -290):
        ball.sety(-290)
        ball_dy *= -1  #invert y dirction

    #ball and players==========
    #collision with p1
    if ball.xcor() < -340 and ball.xcor() > -350 and ball.ycor() > (player1.ycor()-60) and ball.ycor() < (player1.ycor()+ 60):
        ball.setx(-340)
        ball_dx *= -1

    if ball.xcor() > 340 and ball.xcor() < 350 and ball.ycor() > (player2.ycor()-60) and ball.ycor() < ( player2.ycor()+ 60):
        ball.setx(340)
        ball_dx *= -1

    #score ubdate
    if(ball.xcor()> 390):
        ball.goto(x =0 , y=0)
        ball_dx *= -1  #invert x dirction=====
        score.clear()
        p1_score += 1
        score.write(f"player1: {p1_score} player2: {p2_score}", align="center",
                    font=("courier", 14, "normal"))

    if(ball.xcor()< -390 ):
        ball.goto(x= 0 , y=0)
        ball_dx *= -1  #invert x dirctio=====
        score.clear()
        p2_score +=1
        score.write(f"player1: {p1_score} player2: {p2_score}", align="center",
                    font=("courier", 14, "normal"))
