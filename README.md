# Pin-pong
from pygame import *
from random import randint
class GameSprite(sprite.Sprite):
    def __init__(self,player_image, player_x, player_y, size_x, size_y, player_speed):
        super().__init__()
        self.image = transform.scale(image.load(player_image), (size_x, size_y))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y =player_y
    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))
class Player(GameSprite):
    def update(self):
        keys_pressed= key.get_pressed()
        if keys_pressed[K_s] and self.rect.y  < 400:
            self.rect.y  += self.speed
        if keys_pressed[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed
    def update2(self):
        keys_pressed= key.get_pressed()
        if keys_pressed[K_DOWN] and self.rect.y  < 400:
            self.rect.y  += 7
        if keys_pressed[K_UP] and self.rect.y > 5:
            self.rect.y -= 7

window = display.set_mode((700,500))
fon = (255,255,255)
window.fill(fon)
display.set_caption("Пинг понг")
ping1 = Player('wall.png',10,100,50,100,7)
ping2 = Player('wall.png',650,100,50,100,7)
boll = Player('tenis2.jpg',300,300,100,50,3)
font.init()
font = font.Font(None, 70)
win = font.render('Player1 Won', True, (215,215,0))
win2 = font.render('Player2 Won ', True, (215,0,0))
clock = time.Clock()
FPS = 100
speed_x = 3
speed_y = 3


finish = False
game = True
while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    if finish != True:
        window.fill(fon)
        ping1.update()
        ping2.update2()
        ping1.reset()
        ping2.reset()
        boll.reset()
        boll.rect.x += speed_x
        boll.rect.y += speed_y
        if boll.rect.y > 450 or boll.rect.y < 0:
            speed_y *= -1
        if sprite.collide_rect(ping1, boll) or sprite.collide_rect(ping2, boll):
            speed_x *= -1
        if boll.rect.x > 680:
            window.blit(win, (200, 200))
        if boll.rect.x < 5:
            window.blit(win2, (200, 200))
        

           

         
            

        
        display.update()
    clock.tick(FPS)
