import pygame
import sys

# Initialisation de pygame
pygame.init()

# Définition des constantes
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Création de la fenêtre du jeu
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("L'aventure du petit héros")

# Classe du héros
class Hero(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(BLACK)
        self.rect = self.image.get_rect()
        self.rect.center = (SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2)
        self.speed = 5

    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed
        if keys[pygame.K_UP]:
            self.rect.y -= self.speed
        if keys[pygame.K_DOWN]:
            self.rect.y += self.speed

# Création du groupe de sprites pour le héros
all_sprites = pygame.sprite.Group()
hero = Hero()
all_sprites.add(hero)

# Boucle principale du jeu
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Mise à jour et affichage des sprites
    all_sprites.update()

    # Affichage du fond d'écran
    screen.fill(WHITE)

    # Affichage des sprites
    all_sprites.draw(screen)

    # Rafraîchissement de l'écran
    pygame.display.flip()

    # Limite de vitesse de la boucle
    pygame.time.Clock().tick(60)

# Quitter le jeu
pygame.quit()
sys.exit()

