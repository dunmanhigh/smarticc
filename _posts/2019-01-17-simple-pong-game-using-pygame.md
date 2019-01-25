---
title: Simple Pong Game using Pygame
categories: tutorial
tags: game-dev python
author: Zenon Hans Taneka
image: "/assets/img/2019-01-17-simple-pong-game-using-pygame-preview.png"
---

Pong is a classic game that has been played by generations of people. It is a virtual form of the sports ping pong or table tennis.

In this tutorial, we are going to be using pygame to recreate a simplified version of this classic.

First and foremost, we are going to have to install python.
Go to [https://www.python.org/downloads/](https://www.python.org/downloads/) and select the appropriate version for your computer.
During installation, you should make sure that Python is added into your PATH. This will make your life easier in the next step.

Next, we will have to install pygame.
Begin by going to [https://www.pygame.org/wiki/GettingStarted](https://www.pygame.org/wiki/GettingStarted)
Here, you can see a line of code that will install pygame. You need to have Python installed to run this code. So make sure you finished the instructions above first.

On Windows, open your Start menu, by pressing the Windows key, or by pressing the Windows icon on your taskbar, which is likely at the bottom left of your screen. Type "Command Prompt"
On macOS, press ⌘ and spacebar, type in "Terminal" and press enter.
If you are on Linux, you probably already know it. It's Ctrl-Alt-T.

In the command prompt/terminal, type
```python -m pip install -U pygame --user```
and press enter.

If you have installed both Python 2 and 3 before, type
```python3 -m pip install -U pygame --user```
If you don't understand what that means, just skip this.

We have just installed Python and pygame, and now we are ready to start.

Run IDLE by opening your Start menu and typing in IDLE if you are on Windows, or if you are on macOS, ⌘ and spacebar, then type in IDLE and press enter. If you are on Linux, well, you already know it.

Create a new file, with Ctrl-N on Windows or Linux, or for macOS, ⌘ and N.

We first have to import pygame, type in:
```import pygame```
This imports pygame
```
pygame.init()
pygame.font.init()
myfont = pygame.font.SysFont('ArcadeClassic',50)
```
This will initialize pygame. We will also need the font for the scoreboard. ArcadeClassic is a font reminiscent of the classic 8 bit graphics. You would have to install it though, so if you don't want you can also use a font like Arial. Just change the ArcadeClassic to Arial.

We have to specify the size of our game window. To keep it simple, we will use a width of 800 pixels and height of 600 pixels. Let's also give our window a name.
```Python
size = (800,600)
screen = pygame.display.set_mode(size)
screen_rect = screen.get_rect()
pygame.display.set_caption("Pong")
```

In order for us to let the game play, we need to have a time system. In a game's time system, we use ticks to count time.
Go on and create a variable tick
```tick = pygame.time.Clock()```

Let us now work on a player's paddle.
We will start by defining a class called player.
```Python
class player(pygame.sprite.Sprite):
    def __init__(self, no):
```

A paddle looks like a rectangle, so we give it a width 25 pixels and height of 100 pixels.
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.rect = self.image.get_rect()
```

A paddle is white
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
```

Since a paddle's height is 250 pixels, it would have to be 250 pixels down to be at the center of the screen
![paddlecenter.png](https://www.dropbox.com/s/vletkbehrdi8jw1/paddlecenter.png?dl=0&raw=1)
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
```

Make the game draw the paddle
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
        self.rect = self.image.get_rect()
```

If it is player 1, the paddle would be on the left, otherwise, the paddle would be on the right.
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
        self.rect = self.image.get_rect()
        self.no = no
        if no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
```

We need the game to draw the paddles constantly, so we update it every tick.
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
        self.rect = self.image.get_rect()
        self.no = no
        if no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
    def update(self):
        if self.no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif self.no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
```

Finally we allow it to hit the ball
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
        self.rect = self.image.get_rect()
        self.no = no
        if no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
    def update(self):
        if self.no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif self.no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
    def checkcollision(self):
        col = pygame.sprite.collide_rect(self, ball)
        if col:
            ball.velx = -ball.velx
            if ball.velx < 0:
                ball.velx -= 0.5
            else:
                ball.velx += 0.5
```
If the ball collides with a paddle, then the x-velocity of the ball will be reversed as it moves back in the opposite direction. Furthermore, we accelerate the ball a bit each time it hits the paddles.

To make the ball rebounce with more control we make it such that the angle that ball will travel in will be larger when it hits closer the sides of the paddles.
```py
ball.vely = ((ball.posy+12.5) - (self.playery+50))*0.05
```
Take a moment to understand this code. Since the ball is 25 pixels in length, its centre has a y-position of ```ball.posy + 12.5``` because ```ball.posy``` refers to how far it is down. Furthermore, if the ball hits closer the top of the paddle, it would rebound with larger y-velocity, which gives it a larger angle. Vice versa if it hits closer the bottom.

This is the finished code for the paddles
```py
class player(pygame.sprite.Sprite):
    def __init__(self, no):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,100])
        self.image.fill((255,255,255))
        self.playery = 250
        self.rect = self.image.get_rect()
        self.no = no
        if no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
    def update(self):
        if self.no == 1:
            self.rect = pygame.Rect(25, self.playery, 25, 100)
        elif self.no == 2:
            self.rect = pygame.Rect(750, self.playery, 25, 100)
    def checkcollision(self):
        col = pygame.sprite.collide_rect(self, ball)
        if col:
            ball.velx = -ball.velx
            ball.vely = ((ball.posy+12.5) - (self.playery+50))*0.05   
            if ball.velx < 0:
                ball.velx -= 0.5
            else:
                ball.velx += 0.5
```

We are now done with the paddles. Let's now make the ping pong ball
```py
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
```

We simplify the ball by making it a white square.
```
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,25])
        self.image.fill((255,255,255))
```

To make it start from the centre of the screen, we make it start 387.5 pixels from the left, and 287.5 pixels from the top.
![ballcenter.png](https://www.dropbox.com/s/hi6yhiwooq1dxtq/ballcenter.png?dl=0&raw=1)
```py
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,25])
        self.image.fill((255,255,255))
        self.posx = 387.5
        self.posy = 287.5
```

Our ball need to have a velocity for both the x-direction (left to right) and the y-direction (top to bottom). Unfortunately, this is different from the x- and y-axis you might be familiar with. Instead, the origin (0,0) is at the top left corner, and the y-axis is inverted such that down is positive.

We first give it a velocity of 2 pixels to the left, so that the ball can move from its initial position.
```py
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,25])
        self.image.fill((255,255,255))
        self.posx = 387.5
        self.posy = 287.5
        self.velx = -2
        self.vely= 0
```

We tell python to draw the ball
```py
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,25])
        self.image.fill((255,255,255))
        self.posx = 387.5
        self.posy = 287.5
        self.velx = -2
        self.vely= 0
        self.rect = self.image.get_rect()
        self.rect = pygame.Rect(self.posx, self.posy, 25, 25)
```

Now we need the ball to move, so we ask it to change position each tick. It will increase in x-position if it had a positive velocity in the x-direction, and vice versa. Same applies for the y-direction.
```py
class ball(pygame.sprite.Sprite):
    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.Surface([25,25])
        self.image.fill((255,255,255))
        self.posx = 387.5
        self.posy = 287.5
        self.velx = -2
        self.vely= 0
        self.rect = self.image.get_rect()
        self.rect = pygame.Rect(self.posx, self.posy, 25, 25)
    def update(self):
        self.posx += self.velx
        self.posy += self.vely
        self.rect = pygame.Rect(self.posx, self.posy, 25, 25)
```

With the classes that we have now created, we can add each of the player to a group...
```py
playergroup = pygame.sprite.Group()
player1 = player(1)
player2 = player(2)
playergroup.add(player1)
playergroup.add(player2)
```

...and the ball another group of its own.
```py
ballgroup = pygame.sprite.Group()
ball = ball()        
ballgroup.add(ball)
```

Let's now work on the game mechanics. We first tell the game to run, and give each players 0 points to start.
```
player1points = 0
player2points = 0
run = True
```

Start by drawing the objects constantly. We will make the background black in colour.
```py
while run:
    screen.fill((0,0,0))
```

We also have to constantly check whether the ball collides with the paddles.
```py
    player1.checkcollision()
    player2.checkcollision()
```

Move ticker controls how fast the paddles can move.
If both 'W' and 'S' are pressed, we rightly ignore it, since the movements would cancel each other out.
```py
    for event in pygame.event.get():
        move_ticker = 0
    
    if keys[pygame.K_w] and keys[pygame.K_s]:
        if move_ticker == 0:
            move_ticker = 10
```

This makes the left paddle go down when 'S' is pressed...
```py
    elif keys[pygame.K_s]:
        if move_ticker == 0:
            move_ticker = 10
            player1.playery += 5
```

...and up when 'W' is pressed.
```py
    elif keys[pygame.K_w]:
        if move_ticker == 0:
            move_ticker = 10
            player1.playery -= 5
```

Same goes for the second player. But now with the arrow keys.
```py
    if keys[pygame.K_DOWN] and keys[pygame.K_UP]:
        if move_ticker2 == 0:
            move_ticker2 = 10
    elif keys[pygame.K_DOWN]:
        if move_ticker2 == 0:
            move_ticker2 = 10
            player2.playery += 5
    elif keys[pygame.K_UP]:
        if move_ticker2 == 0:
            move_ticker2 = 10
            player2.playery -= 5
```

We make the ball reflect when it hits the top and bottom of the screen
```
    if 0 >= ball.posy:
        ball.vely = -ball.vely
    if ball.posy > 587.5:
        ball.vely = -ball.vely
```

If the ball touches the left side of the screen, the player on the right wins, and vice versa.
```py
    if 0 >= ball.posx:
        ball.posx = 387.5
        ball.posy = 287.5
        ball.velx = 2
        ball.vely = 0
        player2points += 1
    if ball.posx >= 775:
        ball.posx = 387.5
        ball.posy = 287.5
        ball.velx = -2
        ball.vely = 0
        player1points += 1
```

Let's not make the game too crazy. We limit the ball's to have a maximum speed of 45 pixels per tick.
```py
    if ball.velx > 45:
        ball.velx = 45
    elif ball.velx < -45:
        ball.velx = -45
```

We are almost there. Let's now create the midline
```py
    pygame.draw.rect(screen, (255,255,255), [399,0,2,64])
    pygame.draw.rect(screen, (255,255,255), [399,133,2,64])
    pygame.draw.rect(screen, (255,255,255), [399,266,2,64])
    pygame.draw.rect(screen, (255,255,255), [399,400,2,64])
    pygame.draw.rect(screen, (255,255,255), [399,534,2,64])
```

And we also need the scoreboard.
```py
    textsurface = myfont.render(str(player1points), False, (255, 255, 255))
    textsurface2 = myfont.render(str(player2points), False, (255, 255, 255))
    if player1points < 0:
            textsurface = myfont.render('0', False, (255, 255, 255))
    if player2points < 0:
            textsurface2 = myfont.render('0', False, (255, 255, 255))

    screen.blit(textsurface,(335,10))
    screen.blit(textsurface2,(435,10))
```

Finally, we need the game to draw everything while we are playing the game. And we need to redraw all the elements constantly, so we use ```pygame.display.flip()```
```py
    playergroup.update()
    ball.update()
    playergroup.draw(screen)
    ballgroup.draw(screen)
    pygame.display.flip()
    if move_ticker > 0:
        move_ticker -= 1
    if move_ticker2 > 0:
        move_ticker2 -= 1
    tick.tick(60)
```

and end the game when the game is closed.
```py
pygame.quit()
```

And that's it. Save the game (very important!) and press F5 to run it. Go play it with a friend, you have earned yourself a break.