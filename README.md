import pygame
import random

# Inicializar Pygame
pygame.init()

# Configuración de la pantalla
SCREEN_WIDTH = 300
SCREEN_HEIGHT = 600
SCREEN = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Tetris")

# Colores
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Formas de Tetris (cubos)
tetris_shapes = [
    [[1, 1, 1],
     [0, 1, 0]],
    [[0, 1, 1],
     [1, 1, 0]],
    [[1, 1],
     [1, 1]],
    [[1, 1, 1, 1]],
    [[1],
     [1],
     [1],
     [1]],
]

# Función para crear una forma aleatoria
def create_shape():
    shape = random.choice(tetris_shapes)
    color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
    return shape, color

# Función para dibujar una forma en la pantalla
def draw_shape(shape, x, y, color):
    for row in range(len(shape)):
        for col in range(len(shape[row])):
            if shape[row][col] != 0:
                pygame.draw.rect(SCREEN, color, pygame.Rect((x + col) * 30, (y + row) * 30, 30, 30))

# Loop principal del juego
def main():
    clock = pygame.time.Clock()
    shape, color = create_shape()
    x, y = 4, 0

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                quit()

        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            x -= 1
        if keys[pygame.K_RIGHT]:
            x += 1
        if keys[pygame.K_DOWN]:
            y += 1

        SCREEN.fill(BLACK)
        draw_shape(shape, x, y, color)
        pygame.display.update()

        clock.tick(5)

if __name__ == "__main__":
    main()
