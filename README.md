# connect-4
import string
import numpy as np
board = np.zeros((7, 7), dtype=str)
board = np.where(board == "", " ", board)
board[0] = list(string.ascii_uppercase)[:7]
print(board)
player1_choice = input("player 1 choice(X OR O) = ").upper()
player2_choice = input("player 2 choice(X OR O) = ").upper()
if player1_choice == 'X':
    player2_choice = 'O'
else:
    player2_choice = 'X'
    player1_choice = 'O'
col_ind = {'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6}
def player_one_turn():
    col = input("player 1 :Choose a place to play = ").upper()
    column_index = col_ind[col]
    all_cells = board[1:, column_index]
    empty_cells = sum(all_cells == ' ')
    if empty_cells == 6:
        all_cells[-1] = player1_choice
    elif empty_cells > 0:
        all_cells[empty_cells - 7] = player1_choice
    elif empty_cells == 0:
        print("cells is full")
        while empty_cells == 0:
            col = input("player 1 :Choose a place to play = ").upper()
            column_index = col_ind[col]
            all_cells = board[1:, column_index]
            empty_cells = sum(all_cells == ' ')
            if empty_cells != 0:
                all_cells[empty_cells - 7] = player1_choice
            else:
                print("try again")
    print(board)
def player_two_turn():
    col = input("player 2 :Choose a place to play = ").upper()
    column_index = col_ind[col]
    all_cells = board[1:, column_index]
    empty_cells = sum(all_cells == ' ')
    if empty_cells == 6:
        all_cells[-1] = player2_choice
    elif empty_cells > 0:
        all_cells[empty_cells - 7] = player2_choice
    elif empty_cells == 0:
        print("cells is full")
        while empty_cells ==0:
            col = input("player 2 :Choose a place to play = ").upper()
            column_index = col_ind[col]
            all_cells = board[1:, column_index]
            empty_cells = sum(all_cells == ' ')
            if empty_cells != 0:
                all_cells[empty_cells - 7] = player2_choice
            else:
                print("try again")
    print(board)
def score (cells):
    X_score = 0
    O_score = 0
    for cell in cells:
        if cell == 'X':
            X_score += 1
        else:
            if X_score % 4 != 0:
                X_score =X_score - (X_score %4 )
        if cell == 'O':
            O_score += 1
        else:
            if O_score % 4 != 0:
                O_score = O_score - (O_score % 4)
    if player1_choice == 'X':
        player1_score = X_score//4
        player2_score = O_score//4
    else:
        player1_score = O_score // 4
        player2_score = X_score // 4
    return player1_score, player2_score
for i in range(21):
    player_one_turn()
    player_two_turn()
    print(board)
# 6 row
# 7 column
player1_score_total = 0
player2_score_total = 0
for row in range(6):
    cells = board[row+1]
    player1, player2 = score(cells)
    player1_score_total += player1
    player2_score_total += player2

for row in range(7):
    cells = board[1:, row]
    player1, player2 = score(cells)
    player1_score_total += player1
    player2_score_total += player2


print("player one score : {}".format(str(player1_score_total)))
print("player two score : {}".format(str(player2_score_total)))