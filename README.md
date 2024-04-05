import pygame
import sys

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50

# Loop principal do jogo
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Lógica do jogo

    # Desenhar na tela
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))

    # Atualizar a tela
    pygame.display.flip()
import pygame
import sys

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50

# Velocidade do Mario
mario_speed = 5

# Loop principal do jogo
clock = pygame.time.Clock()
while True:
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))

    # Lógica do jogo
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Verifica teclas pressionadas
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        mario_x -= mario_speed
    if keys[pygame.K_RIGHT]:
        mario_x += mario_speed
    if keys[pygame.K_UP]:
        mario_y -= mario_speed
    if keys[pygame.K_DOWN]:
        mario_y += mario_speed

    # Garante que o Mario não saia da tela
    mario_x = max(0, min(SCREEN_WIDTH - mario_image.get_width(), mario_x))
    mario_y = max(0, min(SCREEN_HEIGHT - mario_image.get_height(), mario_y))

    # Atualiza a tela
    pygame.display.flip()

    # Limita a taxa de quadros
    clock.tick(60)
import pygame
import sys

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")
platform_image = pygame.image.load("platform.png")
enemy_image = pygame.image.load("enemy.png")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50
mario_speed = 5
mario_jump = False
mario_jump_count = 10

# Definição da posição inicial dos inimigos
enemy_x = 600
enemy_y = SCREEN_HEIGHT - enemy_image.get_height() - 50
enemy_speed = 3

# Lista de plataformas
platforms = [(200, 400), (400, 300), (600, 200)]

# Loop principal do jogo
clock = pygame.time.Clock()
while True:
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))
    screen.blit(enemy_image, (enemy_x, enemy_y))

    # Desenhar plataformas
    for platform in platforms:
        screen.blit(platform_image, platform)

    # Lógica do jogo
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Movimento do Mario
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        mario_x -= mario_speed
    if keys[pygame.K_RIGHT]:
        mario_x += mario_speed

    # Lógica de pulo do Mario
    if not mario_jump:
        if keys[pygame.K_SPACE]:
            mario_jump = True
    else:
        if mario_jump_count >= -10:
            neg = 1
            if mario_jump_count < 0:
                neg = -1
            mario_y -= (mario_jump_count ** 2) * 0.5 * neg
            mario_jump_count -= 1
        else:
            mario_jump = False
            mario_jump_count = 10

    # Atualizar posição dos inimigos
    enemy_x -= enemy_speed
    if enemy_x <= 0:
        enemy_x = SCREEN_WIDTH
    # Verificar colisão com o Mario
    if (mario_x + mario_image.get_width() > enemy_x and mario_x < enemy_x + enemy_image.get_width() and
            mario_y + mario_image.get_height() > enemy_y and mario_y < enemy_y + enemy_image.get_height()):
        # Código de colisão (por exemplo, Game Over)
        pass

    # Verificar colisão com as plataformas
    for platform in platforms:
        if (mario_y + mario_image.get_height() >= platform[1] and mario_y + mario_image.get_height() <= platform[1] + platform_image.get_height()
                and mario_x + mario_image.get_width() >= platform[0] and mario_x <= platform[0] + platform_image.get_width()):
            mario_jump = False
            mario_jump_count = 10

    # Garante que o Mario não saia da tela
    mario_x = max(0, min(SCREEN_WIDTH - mario_image.get_width(), mario_x))
    mario_y = max(0, min(SCREEN_HEIGHT - mario_image.get_height(), mario_y))

    # Atualiza a tela
    pygame.display.flip()

    # Limita a taxa de quadros
    clock.tick(60)
import pygame
import sys
import random

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
FONT_SIZE = 36

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")
platform_image = pygame.image.load("platform.png")
enemy_image = pygame.image.load("enemy.png")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50
mario_speed = 5
mario_jump = False
mario_jump_count = 10

# Definição da posição inicial dos inimigos
enemies = []
for _ in range(3):
    enemy_x = random.randint(100, SCREEN_WIDTH - 100)
    enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
    enemy_speed = random.randint(2, 4)
    enemies.append((enemy_x, enemy_y, enemy_speed))

# Lista de plataformas
platforms = [(200, 400), (400, 300), (600, 200)]

# Variáveis de jogo
score = 0
lives = 3
font = pygame.font.Font(None, FONT_SIZE)

# Loop principal do jogo
clock = pygame.time.Clock()
while True:
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))

    # Desenhar plataformas
    for platform in platforms:
        screen.blit(platform_image, platform)

    # Desenhar inimigos
    for enemy in enemies:
        screen.blit(enemy_image, (enemy[0], enemy[1]))

    # Desenhar informações de jogo
    score_text = font.render(f"Score: {score}", True, BLACK)
    screen.blit(score_text, (20, 20))
    lives_text = font.render(f"Lives: {lives}", True, BLACK)
    screen.blit(lives_text, (20, 60))

    # Lógica do jogo
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Movimento do Mario
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        mario_x -= mario_speed
    if keys[pygame.K_RIGHT]:
        mario_x += mario_speed

    # Lógica de pulo do Mario
    if not mario_jump:
        if keys[pygame.K_SPACE]:
            mario_jump = True
    else:
        if mario_jump_count >= -10:
            neg = 1
            if mario_jump_count < 0:
                neg = -1
            mario_y -= (mario_jump_count ** 2) * 0.5 * neg
            mario_jump_count -= 1
        else:
            mario_jump = False
            mario_jump_count = 10

    # Atualizar posição dos inimigos
    for i, enemy in enumerate(enemies):
        enemy_x, enemy_y, enemy_speed = enemy
        enemy_x -= enemy_speed
        enemies[i] = (enemy_x, enemy_y, enemy_speed)
        # Verificar colisão com o Mario
        if (mario_x + mario_image.get_width() > enemy_x and mario_x < enemy_x + enemy_image.get_width() and
                mario_y + mario_image.get_height() > enemy_y and mario_y < enemy_y + enemy_image.get_height()):
            # Decrementa as vidas e reposiciona o inimigo
            lives -= 1
            enemy_x = SCREEN_WIDTH
            enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
            enemies[i] = (enemy_x, enemy_y, enemy_speed)

    # Verificar colisão com as plataformas
    for platform in platforms:
        if (mario_y + mario_image.get_height() >= platform[1] and mario_y + mario_image.get_height() <= platform[1] + platform_image.get_height()
                and mario_x + mario_image.get_width() >= platform[0] and mario_x <= platform[0] + platform_image.get_width()):
            mario_jump = False
            mario_jump_count = 10

    # Garante que o Mario não saia da tela
    mario_x = max(0, min(SCREEN_WIDTH - mario_image.get_width(), mario_x))
    mario_y = max(0, min(SCREEN_HEIGHT - mario_image.get_height(), mario_y))

    # Atualiza a tela
    pygame.display.flip()

    # Limita a taxa de quadros
    clock.tick(60)
import pygame
import sys
import random

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
FONT_SIZE = 36

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")
platform_image = pygame.image.load("platform.png")
enemy_image = pygame.image.load("enemy.png")
coin_image = pygame.image.load("coin.png")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50
mario_speed = 5
mario_jump = False
mario_jump_count = 10
mario_attack = False
mario_attack_cooldown = 0
mario_score = 0

# Definição da posição inicial dos inimigos
enemies = []
for _ in range(3):
    enemy_x = random.randint(100, SCREEN_WIDTH - 100)
    enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
    enemy_speed = random.randint(2, 4)
    enemies.append((enemy_x, enemy_y, enemy_speed))

# Lista de plataformas
platforms = [(200, 400), (400, 300), (600, 200)]

# Lista de moedas
coins = []
for _ in range(5):
    coin_x = random.randint(100, SCREEN_WIDTH - 100)
    coin_y = random.randint(50, SCREEN_HEIGHT - 200)
    coins.append((coin_x, coin_y))

# Variáveis de jogo
score = 0
lives = 3
font = pygame.font.Font(None, FONT_SIZE)

# Loop principal do jogo
clock = pygame.time.Clock()
while True:
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))

    # Desenhar plataformas
    for platform in platforms:
        screen.blit(platform_image, platform)

    # Desenhar inimigos
    for enemy in enemies:
        screen.blit(enemy_image, (enemy[0], enemy[1]))

    # Desenhar moedas
    for coin in coins:
        screen.blit(coin_image, (coin[0], coin[1]))

    # Desenhar informações de jogo
    score_text = font.render(f"Score: {mario_score}", True, BLACK)
    screen.blit(score_text, (20, 20))
    lives_text = font.render(f"Lives: {lives}", True, BLACK)
    screen.blit(lives_text, (20, 60))

    # Lógica do jogo
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Movimento do Mario
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        mario_x -= mario_speed
    if keys[pygame.K_RIGHT]:
        mario_x += mario_speed

    # Lógica de pulo do Mario
    if not mario_jump:
        if keys[pygame.K_SPACE]:
            mario_jump = True
    else:
        if mario_jump_count >= -10:
            neg = 1
            if mario_jump_count < 0:
                neg = -1
            mario_y -= (mario_jump_count ** 2) * 0.5 * neg
            mario_jump_count -= 1
        else:
            mario_jump = False
            mario_jump_count = 10

    # Lógica de ataque do Mario
    if mario_attack_cooldown > 0:
        mario_attack_cooldown -= 1

    if keys[pygame.K_SPACE] and mario_attack_cooldown == 0:
        mario_attack = True
        mario_attack_cooldown = 30  # Cooldown de 30 frames

    # Atualizar posição dos inimigos
    for i, enemy in enumerate(enemies):
        enemy_x, enemy_y, enemy_speed = enemy
        enemy_x -= enemy_speed
        enemies[i] = (enemy_x, enemy_y, enemy_speed)
        # Verificar colisão com o Mario
        if (mario_x + mario_image.get_width() > enemy_x and mario_x < enemy_x + enemy_image.get_width() and
                mario_y + mario_image.get_height() > enemy_y and mario_y < enemy_y + enemy_image.get_height()):
            # Decrementa as vidas e reposiciona o inimigo
            lives -= 1
            enemy_x = SCREEN_WIDTH
            enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
            enemies[i] = (enemy_x, enemy_y, enemy_speed)

    # Verificar colisão com as plataformas
    for platform in platforms:
        if (mario_y + mario_image.get_height() >= platform[1] and mario_y + mario_image.get_height() <= platform[1] + platform_image.get_height()
                and mario_x + mario_image.get_width() >= platform[0] and mario_x <= platform[0] + platform_image.get_width()):
            mario_jump = False
            mario_jump_count = 10

    # Verificar colisão com as moedas
    for coin in coins:
        if (mario_x + mario_image.get_width() > coin[0] and mario_x < coin[0] + coin_image.get_width() and
                mario_y + mario_image.get_height() > coin[1] and mario_y < coin[1] + coin_image.get_height()):
            mario_score += 10
            coins.remove(coin)

    # Garante que o Mario não saia da tela
    mario_x = max(0, min(SCREEN_WIDTH - mario_image.get_width(), mario_x))
    mario_y = max(0, min(SCREEN_HEIGHT - mario_image.get_height(), mario_y))

    # Atualiza a tela
    pygame.display.flip()

    # Limita a taxa de quadros
    clock.tick(60)
import pygame
import sys
import random

# Inicialização do Pygame
pygame.init()

# Definição de variáveis globais
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
FONT_SIZE = 36

# Configuração da tela
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Mario Game")

# Carregamento de imagens
background_image = pygame.image.load("background.jpg")
mario_image = pygame.image.load("mario.png")
platform_image = pygame.image.load("platform.png")
enemy_image = pygame.image.load("enemy.png")
coin_image = pygame.image.load("coin.png")

# Carregamento de sons
jump_sound = pygame.mixer.Sound("jump.wav")
coin_sound = pygame.mixer.Sound("coin.wav")
game_over_sound = pygame.mixer.Sound("game_over.wav")

# Definição da posição inicial do Mario
mario_x = 50
mario_y = SCREEN_HEIGHT - mario_image.get_height() - 50
mario_speed = 5
mario_jump = False
mario_jump_count = 10
mario_attack = False
mario_attack_cooldown = 0
mario_score = 0

# Definição da posição inicial dos inimigos
enemies = []
for _ in range(3):
    enemy_x = random.randint(100, SCREEN_WIDTH - 100)
    enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
    enemy_speed = random.randint(2, 4)
    enemies.append((enemy_x, enemy_y, enemy_speed))

# Lista de plataformas
platforms = [(200, 400), (400, 300), (600, 200)]

# Lista de moedas
coins = []
for _ in range(5):
    coin_x = random.randint(100, SCREEN_WIDTH - 100)
    coin_y = random.randint(50, SCREEN_HEIGHT - 200)
    coins.append((coin_x, coin_y))

# Variáveis de jogo
score = 0
lives = 3
font = pygame.font.Font(None, FONT_SIZE)

# Loop principal do jogo
clock = pygame.time.Clock()
game_over = False
while not game_over:
    screen.fill(WHITE)
    screen.blit(background_image, (0, 0))
    screen.blit(mario_image, (mario_x, mario_y))

    # Desenhar plataformas
    for platform in platforms:
        screen.blit(platform_image, platform)

    # Desenhar inimigos
    for enemy in enemies:
        screen.blit(enemy_image, (enemy[0], enemy[1]))

    # Desenhar moedas
    for coin in coins:
        screen.blit(coin_image, (coin[0], coin[1]))

    # Desenhar informações de jogo
    score_text = font.render(f"Score: {mario_score}", True, BLACK)
    screen.blit(score_text, (20, 20))
    lives_text = font.render(f"Lives: {lives}", True, BLACK)
    screen.blit(lives_text, (20, 60))

    # Lógica do jogo
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Movimento do Mario
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        mario_x -= mario_speed
    if keys[pygame.K_RIGHT]:
        mario_x += mario_speed

    # Lógica de pulo do Mario
    if not mario_jump:
        if keys[pygame.K_SPACE]:
            mario_jump = True
            jump_sound.play()
    else:
        if mario_jump_count >= -10:
            neg = 1
            if mario_jump_count < 0:
                neg = -1
            mario_y -= (mario_jump_count ** 2) * 0.5 * neg
            mario_jump_count -= 1
        else:
            mario_jump = False
            mario_jump_count = 10

    # Lógica de ataque do Mario
    if mario_attack_cooldown > 0:
        mario_attack_cooldown -= 1

    if keys[pygame.K_SPACE] and mario_attack_cooldown == 0:
        mario_attack = True
        mario_attack_cooldown = 30  # Cooldown de 30 frames

    # Atualizar posição dos inimigos
    for i, enemy in enumerate(enemies):
        enemy_x, enemy_y, enemy_speed = enemy
        enemy_x -= enemy_speed
        enemies[i] = (enemy_x, enemy_y, enemy_speed)
        # Verificar colisão com o Mario
        if (mario_x + mario_image.get_width() > enemy_x and mario_x < enemy_x + enemy_image.get_width() and
                mario_y + mario_image.get_height() > enemy_y and mario_y < enemy_y + enemy_image.get_height()):
            # Decrementa as vidas e reposiciona o inimigo
            lives -= 1
            enemy_x = SCREEN_WIDTH
            enemy_y = random.randint(50, SCREEN_HEIGHT - 200)
            enemies[i] = (enemy_x, enemy_y, enemy_speed)

    # Verificar colisão com as plataformas
    for platform in platforms:
        if (mario_y + mario_image.get_height() >= platform[1] and mario_y + mario_image.get_height() <= platform[1] + platform_image.get_height()
                and mario_x + mario_image.get_width() >= platform[0] and mario_x <= platform[0] + platform_image.get_width()):
            mario_jump = False
            mario_jump_count = 10

    # Verificar colisão com as moedas
    for coin in coins:
        if (mario_x + mario_image.get_width() > coin[0] and mario_x < coin[0] + coin_image.get_width() and
                mario_y + mario_image.get_height() > coin[1] and mario_y < coin[1] + coin_image.get_height()):
            mario_score += 10
            coins.remove(coin)
            coin_sound.play()

    # Garante que o Mario não saia da tela
    mario_x = max(0, min(SCREEN_WIDTH - mario_image.get_width(), mario_x))
    mario_y = max(0, min(SCREEN_HEIGHT - mario_image.get_height(), mario_y))

    # Checar condição de game over
    if lives <= 0:
        game_over_sound.play()
        game_over_text = font.render("GAME OVER", True, BLACK)
        screen.blit(game_over_text, (SCREEN_WIDTH // 2 - 100, SCREEN_HEIGHT // 2 - 50))
        pygame.display.flip()
        pygame.time.wait(2000)  # Espera 2 segundos
