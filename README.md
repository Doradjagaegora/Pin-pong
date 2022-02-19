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
clock = time.Clock()
FPS = 100



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

        
        display.update()
    clock.tick(FPS)
