import pygame
import sys

# Define the colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Define the size of the game board
BOARD_SIZE = 3

# Define the size of the window
WINDOW_SIZE = 600

# Define the size of the squares
SQUARE_SIZE = WINDOW_SIZE // BOARD_SIZE

# Initialize the game
pygame.init()

# Set up the display
DISPLAY = pygame.display.set_mode((WINDOW_SIZE, WINDOW_SIZE))

# Set up the clock
CLOCK = pygame.time.Clock()

# Define the game board
board = [[None for _ in range(BOARD_SIZE)] for _ in range(BOARD_SIZE)]

# Define the gobblers
gobblers = {'small': 1, 'medium': 2, 'large': 3}

def draw_board():
    DISPLAY.fill(WHITE)
    for i in range(1, BOARD_SIZE):
        pygame.draw.line(DISPLAY, BLACK, (0, i * SQUARE_SIZE), (WINDOW_SIZE, i * SQUARE_SIZE))
        pygame.draw.line(DISPLAY, BLACK, (i * SQUARE_SIZE, 0), (i * SQUARE_SIZE, WINDOW_SIZE))
    pygame.display.update()

def place_gobbler(size, row, col, player):
    if board[row][col] is None or gobblers[size] > gobblers[board[row][col][0]]:
        board[row][col] = (size, player)

def check_win():
    for row in board:
        if row.count(row[0]) == len(row) and row[0] is not None:
            return row[0][1]
    for col in range(len(board[0])):
        check = []
        for row in board:
            check.append(row[col])
        if check.count(check[0]) == len(check) and check[0] is not None:
            return check[0][1]
    if board[0][0] == board[1][1] == board[2][2] and board[0][0] is not None:
        return board[0][0][1]
    if board[0][2] == board[1][1] == board[2][0] and board[0][2] is not None:
        return board[0][2][1]
    return None

def game_loop():
    draw_board()
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                mouseX, mouseY = pygame.mouse.get_pos()
                row, col = mouseY // SQUARE_SIZE, mouseX // SQUARE_SIZE
                place_gobbler('large', row, col, 'player1')
                winner = check_win()
                if winner is not None:
                    print(f'{winner} wins!')
                    pygame.quit()
                    sys.exit()
        pygame.display.update()
        CLOCK.tick(60)

game_loop()
