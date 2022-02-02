import pygame as pg
import random
import tkinter as tk
import time
pg.init() #initializing pygame

#colors
black = (0,0,0)
white = (255, 255, 255)
red = (255, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)

#images
pg.display.set_caption("Don't Step - A Pygame Creation")
background = pg.image.load('road.jpg')
bg = background.get_size()

#window setting
display = pg.display.set_mode((bg))
length, breadth = bg
start_x, start_y = 0, breadth/2 #starting coordinates of ball
clock = pg.time.Clock()

def restart():
    gameloop()

def QuitMsg(Title, LeftButton, RightButton):
    #import tkinter as tk
    msg_window = tk.Tk()
    msg_window.configure(background='light green')
    msg_window.title(str(Title))
    msg_window.geometry('200x70')
    leftbutton = tk.Button(msg_window, text=str(LeftButton), fg='blue', bg='pink',
                           command=exit, height=1, width=5)
    leftbutton.grid(row=1, column=1)
    rightbutton = tk.Button(msg_window, text=str(RightButton), fg='blue', bg='pink',
                            command=msg_window.destroy, height=1, width=5)
    rightbutton.grid(row=1, column=2)
    msg_window.mainloop()

class Player(pg.sprite.Sprite):
    def __init__(self, x, y):
        super(Player, self).__init__()
        self.x = x
        self.y = y
        self.image = pg.image.load('shoes (2).png')
        self.width = 50
        self.height = 50
        self.rect = self.image.get_rect()

    def renderPlayer(self):
        display.blit(self.image, (self.x, self.y))
    

class Hurdle(pg.sprite.Sprite):
    def __init__(self, m_x, m_y):
        super(Hurdle, self).__init__()
        self.m_x = m_x
        self.m_y = m_y
        self.image = pg.image.load("money1.png")
        self.rect = self.image.get_rect()
        
    def renderHurdle(self):
        display.blit(self.image, (self.m_x, self.m_y))


def collision(x1,y1,w1,h1,x2,y2,w2,h2): 
    if (x2+w2>=x1>=x2 and y2+h2>=y1>=y2):
        return True
    elif (x2+w2>=x1+w1>=x2 and y2+h2>=y1>=y2):
        return True
    elif (x2+w2>=x1>=x2 and y2+h2>=y1+h1>=y2):
        return True
    elif (x2+w2>=x1+w1>=x2 and y2+h2>=y1+h1>=y2):
        return True
    else:
        return False

def gameloop(LEVEL=1) :

    print("Hey! Welcome to Don't Step! Press space to jump, right and left to move./nThere are 4 levels.")
    print("Good luck! Wait for further instructions.")

    LEVEL = 1 #game level#

    play = Player(start_x, start_y)

    '''following few lines are only for definition of hurdles'''
    hurdles_x = [x * 100/LEVEL * 1.20 for x in range (1,10+LEVEL)] #x coordinates of hurdle

    money_hurdles = []

    for i in range(0,9):
        money_note = Hurdle(hurdles_x[i], random.randint(0,500))
        money_hurdles.append(money_note)
    '''hurdles defined and contained in a list'''
    
    x_change = 0  #initial change in x coordinate of player
    y_change = 0  #initial change in y coordinate of player
    
    Exit = True   #driver code starts
    while Exit and LEVEL < 4 :
        
        for event in pg.event.get():
            if event.type == pg.QUIT:
                QuitMsg("Quit Game?", "Quit", "No")
            
            if event.type == pg.KEYDOWN:
                if event.key == pg.K_RIGHT:
                    x_change = 4
                elif event.key == pg.K_LEFT:
                    x_change = -4
                else:
                    x_change = 0
                if event.key == pg.K_SPACE:
                    y_change = -7
                else:
                    y_change = 0
            if event.type == pg.MOUSEMOTION:
                y_change = 0
                
            if event.type == pg.KEYUP and event.key == pg.K_SPACE :
                y_change = 7
            if event.type == pg.KEYUP:
                if event.key == pg.K_RIGHT or event.key == pg.K_LEFT :
                    x_change = 0
                    y_change = 7

        display.fill(white)
        display.blit(background, (0,0))
        play.x += x_change
        play.y += y_change

        for note in money_hurdles :
            if collision(play.x, play.y, play.width, play.height, note.m_x, note.m_y, note.rect.width, note.rect.height) :
                print("You STEPPED ON GODDESS LAXMI. Your punishment is to wait.. until game starts!")
                time.sleep(5)
                gameloop(LEVEL)  

        for note in money_hurdles :
            note.renderHurdle()
        play.renderPlayer()

        if play.x > (length - play.width) :
            print("Level complete!")
            inp = input("Enter N for next level or Q to quit: ")
            if inp.upper() == 'N' :
                if LEVEL+1 == 5 :
                    print("Aur kitna kheloge?")
                else:
                    print("Next Level starting..")
                    time.sleep(3)
                    gameloop(LEVEL+1)
                
            elif inp.upper() == 'Q' :
                Exit = False
            else :
                print("Invalid")
                Exit = True            
            
        if play.y > (breadth - play.height) :
            print('You Crashed!')

            time.sleep(3)

            
            restart()
            

        clock.tick(60)
        pg.display.update()
    

gameloop()
pg.quit()

