# 666
from pygame import *
from random import*

mixer.init()
mixer.music.set_volume(0.1)
font.init()
game_font = font.Font(None,50)
green = (255,215,0)
red = (180,0,0)
skr = display.set_mode((1500,990))
display.set_caption("/                                                                                                                                                                                                                                             Шутер")
back = transform.scale(image.load('wallhaven-7pqr2e.jpg'), (1500,990))




class GameSprite(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y,h,w, speed):
        super().__init__()
        self.image = transform.scale(image.load(player_image),(h,w))
        self.speed = speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y
    def reset(self):
        skr.blit(self.image,(self.rect.x, self.rect.y))
class Player(GameSprite):
    def update(self):
        keys = key.get_pressed()
        if keys[K_UP] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_DOWN] and self.rect.y < 980:
            self.rect.y += self.speed
    def update_2(self):
        keys = key.get_pressed()
        if keys[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_s] and self.rect.y <= 800:
            self.rect.y += self.speed
'''class ball(GameSprite):
    def rew(self):
        self.rect.x += self.speed
    def wer(self):
        self.speed = 30
        self.rect.x -= self.speed'''

sprite_1 = Player('asteroid.png',400,700,50,50,10)
sprite_2 = Player('wall_1.png',200,700,40,250,20)
sprite_3 = Player('wall_1.png',1300,700,40,250,20)
clock = time.Clock()
GAME = True
finish = False
speed_x = 3
speed_y = 3
while GAME:
    for i in event.get():
        if i.type == QUIT:
            GAME = False
    
    if finish != True:
        skr.blit(back,(0,0))
        sprite_3.reset()
        sprite_3.update()

        sprite_2.reset()
        sprite_2.update_2()

        sprite_1.reset()
        sprite_1.rect.x += speed_x
        sprite_1.rect.y += speed_y
        if sprite_1.rect.colliderect(sprite_2.rect):
            speed_x *= -1

        if sprite_1.rect.colliderect(sprite_3.rect):
            speed_x *= -1

        if sprite_1.rect.y > 800:
            speed_y *= -1
        
        if sprite_1.rect.y < 200:
            speed_y *= -1
        
        
        if sprite_1.rect.x > 1900:
            finish = True
            lose_text = game_font.render('Правый проиграл', True,(255,0,0))
            skr.blit(lose_text,(750,490))

        if sprite_1.rect.x < 100:
            finish = True
            lose_text = game_font.render('Левый проиграл', True,(255,0,0))
            skr.blit(lose_text,(750,490))
        
        


    display.update()
    clock.tick(50)


