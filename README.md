naruto_image = pygame.image.load('assets/images/naruto.png')
naruto_rect = naruto_image.get_rect()
naruto_rect.topleft = (100, 100)

enemy_image = pygame.image.load('assets/images/enemy.png')
enemy_rect = enemy_image.get_rect()
enemy_rect.topleft = (400, 300)

sakura_image = pygame.image.load('assets/images/sakura.png')
sakura_rect = sakura_image.get_rect()
sakura_rect.topleft = (200, 200)

# Define dimensions
dimensions = ["Heroic", "Rogue", "Peaceful", "Technological", "Dark", "Sage", "Diplomat"]
current_dimension = 0

def draw_dimension_background(screen, dimension):
    if dimension == "Heroic":
        screen.fill(BLUE)
    elif dimension == "Rogue":
        screen.fill(RED)
    elif dimension == "Peaceful":
        screen.fill(GREEN)
    elif dimension == "Technological":
        screen.fill(GRAY)
    elif dimension == "Dark":
        screen.fill(BLACK)
    elif dimension == "Sage":
        screen.fill(GOLD)
    elif dimension == "Diplomat":
        screen.fill(ORANGE)

# Movement speed
speed = 5

# Basic attack function
def attack(target_rect):
    # Simple collision check
    if naruto_rect.colliderect(target_rect):
        print("Hit!")

# Main game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:  # Switch dimension on space key press
                current_dimension = (current_dimension + 1) % len(dimensions)
            elif event.key == pygame.K_a:  # 'a' key for attack
                attack(enemy_rect)

    # Get the keys currently pressed
    keys = pygame.key.get_pressed()
    
    # Update Naruto's position based on keys
    if keys[pygame.K_LEFT]:
        naruto_rect.x -= speed
    if keys[pygame.K_RIGHT]:
        naruto_rect.x += speed
    if keys[pygame.K_UP]:
        naruto_rect.y -= speed
    if keys[pygame.K_DOWN]:
        naruto_rect.y += speed

    # Clear the screen
    draw_dimension_background(screen, dimensions[current_dimension])
    
    # Draw characters
    screen.blit(naruto_image, naruto_rect.topleft)
    screen.blit(enemy_image, enemy_rect.topleft)
    screen.blit(sakura_image, sakura_rect.topleft)
    
    # Update the display
    pygame.display.flip()

# Quit Pygame
pygame.quit()
sys.exit()
