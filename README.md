import pygame
import random

# Constants
WIDTH, HEIGHT = 800, 600
FPS = 60
GRID_SIZE = 20
SCALE = 30

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
BROWN = (139, 69, 19)

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Terrain Generation")
clock = pygame.time.Clock()

# Generate random terrain
terrain = [[random.randint(0, 1) for _ in range(WIDTH // GRID_SIZE)] for _ in range(HEIGHT // GRID_SIZE)]

def generate_terrain():
    for y in range(len(terrain)):
        for x in range(len(terrain[0])):
            terrain[y][x] = random.randint(0, 1)

# Main game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                generate_terrain()

    # Draw the terrain
    screen.fill(WHITE)
    for y in range(len(terrain)):
        for x in range(len(terrain[0])):
            color = GREEN if terrain[y][x] == 0 else BROWN
            pygame.draw.rect(screen, color, (x * GRID_SIZE, y * GRID_SIZE, GRID_SIZE, GRID_SIZE))

    pygame.display.flip()
    clock.tick(FPS)

# Quit the game
pygame.quit()

