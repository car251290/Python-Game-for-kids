# Python-Game-for-kids
Python game for children where I use it for them to understand better the basic of the program

#How to make a Python game.

The subject class I will build with the chlidren is a simple python game that use an if statement an accounter for the score the first step is that they will download and try the basic concepts of the game.

I will use this page as a resorces to the game: https://www.pygame.org/news
but to download and start I will show them the fisrt to the end how to make it.

this the code I will use for make the kids will change some of the design as color and the size of the window as they choose.
# my Goal 
They Have to understand the if statemnet and how to make a declaration function, and change the color of the window with code


# import the pygame
 import pygame
# Call this function so the Pygame library can initialize itself
pygame.init()

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 000)

# Set the width and height of each snake segment
segment_width = 15
segment_height = 15
# Margin between each segment
segment_margin = 3

# Set initial speed
x_change = segment_width + segment_margin
y_change = 0


class Segment(pygame.sprite.Sprite):
   # these are the Methods
   # Constructor function
    def __init__(self, x, y):
   # Call the parent's constructor
        super().__init__()
        
   # Set of the height and the width
        self.image = pygame.Surface([segment_width, segment_height])
        self.image.fill(WHITE)

   # Making the our of the top-left the passed.
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y



# Create an 800x600 sized screen
screen = pygame.display.set_mode([800, 600])

# Set the title of the window
pygame.display.set_caption('Snake Example')

allspriteslist = pygame.sprite.Group()

# Create an initial snake
snake_segments = []
for i in range(15):
    x = 250 - (segment_width + segment_margin) * i
    y = 30
    segment = Segment(x, y)
    snake_segments.append(segment)
    allspriteslist.add(segment)

# The clock of the time of the game
clock = pygame.time.Clock()
done = False

while not done:

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True
   # Set the speedWe want the speed to be enough that we move a full
   # Segment, plus the margin.
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                x_change = (segment_width + segment_margin) * -1
                y_change = 0
            if event.key == pygame.K_RIGHT:
                x_change = (segment_width + segment_margin)
                y_change = 0
            if event.key == pygame.K_UP:
                x_change = 0
                y_change = (segment_height + segment_margin) * -1
            if event.key == pygame.K_DOWN:
                x_change = 0
                y_change = (segment_height + segment_margin)

  # Get rid of last segment of the snake
  # pop() command removes last item in list
    old_segment = snake_segments.pop()
    allspriteslist.remove(old_segment)

  # The segment and possition of the snake
    x = snake_segments[0].rect.x + x_change
    y = snake_segments[0].rect.y + y_change
    segment = Segment(x, y)

  # Insert new segment into the list
    snake_segments.insert(0, segment)
    allspriteslist.add(segment)

 # Draw everything
 # Clear screen
    screen.fill(BLACK)

    allspriteslist.draw(screen)

  # Flip screen
    pygame.display.flip()

  # Pause
    clock.tick(5)
# for Pyhton understand when to quit
pygame.quit()


