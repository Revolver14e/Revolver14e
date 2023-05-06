- 👋 Hi, I’m @Revolver14e
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Revolver14e/Revolver14e is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import os

# Initialize Pygame
pygame.init()

# Set up the window
window_width = 640
window_height = 480
window = pygame.display.set_mode((window_width, window_height))

# Load the images
player_image = pygame.image.load(os.path.join('images', 'player.png')).convert_alpha()
platform_image = pygame.image.load(os.path.join('images', 'platform.png')).convert_alpha()

# Set up the player
player_x = 100
player_y = 100
player_width = player_image.get_width()
player_height = player_image.get_height()
player_vel_x = 0
player_vel_y = 0

# Set up the platform
platform_x = 200
platform_y = 400
platform_width = platform_image.get_width()
platform_height = platform_image.get_height()

# Set up the game loop
clock = pygame.time.Clock()
game_running = True

while game_running:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player_vel_x = -5
            elif event.key == pygame.K_RIGHT:
                player_vel_x = 5
            elif event.key == pygame.K_SPACE:
                player_vel_y = -10

    # Update the player's position
    player_x += player_vel_x
    player_y += player_vel_y

    # Apply gravity
    player_vel_y += 1

    # Handle collisions
    if player_x < 0:
        player_x = 0
    elif player_x > window_width - player_width:
        player_x = window_width - player_width

    if player_y < 0:
        player_y = 0
    elif player_y > window_height - player_height:
        player_y = window_height - player_height

    if player_x + player_width > platform_x and player_x < platform_x + platform_width and player_y + player_height > platform_y and player_y < platform_y + platform_height:
        player_y = platform_y - player_height
        player_vel_y = 0

    # Draw the sprites
    window.fill((0, 0, 0))
    window.blit(player_image, (player_x, player_y))
    window.blit(platform_image, (platform_x, platform_y))

    # Update the display
    pygame.display.update()

    # Tick the clock
    clock.tick(60)

# Quit Pygame
pygame.quit()

