import pygame
import random

# Initialize pygame
pygame.init()

# Set up display
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Simple Racing Game")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# Clock and FPS
clock = pygame.time.Clock()
FPS = 60

# Car settings
CAR_WIDTH = 50
CAR_HEIGHT = 100
car_img = pygame.Surface((CAR_WIDTH, CAR_HEIGHT))
car_img.fill(RED)

# Road settings
ROAD_WIDTH = 400
ROAD_LEFT = (WIDTH - ROAD_WIDTH) // 2
ROAD_RIGHT = ROAD_LEFT + ROAD_WIDTH

# Game variables
car_x = WIDTH // 2 - CAR_WIDTH // 2
car_y = HEIGHT - CAR_HEIGHT - 10
car_speed = 5
game_running = True

# Function to draw the road
def draw_road():
    pygame.draw.rect(screen, (100, 100, 100), (ROAD_LEFT, 0, ROAD_WIDTH, HEIGHT))
    pygame.draw.rect(screen, (255, 255, 255), (ROAD_LEFT + ROAD_WIDTH // 2 - 5, 0, 10, HEIGHT))

# Function to move the car
def move_car(keys, car_x):
    if keys[pygame.K_LEFT] and car_x > ROAD_LEFT:
        car_x -= car_speed
    if keys[pygame.K_RIGHT] and car_x < ROAD_RIGHT - CAR_WIDTH:
        car_x += car_speed
    return car_x

# Main game loop
while game_running:
    screen.fill(WHITE)
    draw_road()
    
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_running = False

    # Get key states
    keys = pygame.key.get_pressed()

    # Move the car
    car_x = move_car(keys, car_x)

    # Draw the car
    screen.blit(car_img, (car_x, car_y))

    # Update the display
    pygame.display.update()

    # Set the frame rate
    clock.tick(FPS)

# Quit pygame
pygame.quit()
