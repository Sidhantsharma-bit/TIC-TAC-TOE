# TIC TAC TOE
 

winner=None

current_player="X"

game_still_going = True

board = ["-", "-", "-", 
        "-", "-", "-", 
        "-", "-", "-",]

def display_board():
    print(board[0] + "|" + board[1] + "|" + board[2])
    print(board[3] + "|" + board[4] + "|" + board[5])
    print(board[6] + "|" + board[7] + "|" + board[8])

def play_game():

    display_board()

    while game_still_going:

        handle_turn(current_player)

        check_is_game_over()

        flip_player()

    if winner=="X" or winner=="O":
        print(winner + " Won.")
    elif winner==None:
        print("Tie.")

def handle_turn(player):
    print(player + "'s turn")

    position = input("Choose a position between 1-9: ")

    valid = False
    while not valid:

        while position not in ["1", "2", "3", "4", "5", "6", "7", "8", "9"]:
            position = input("Choose between 1-9: ")

        position = int(position) - 1

        if position =="-":
            valid = True
        else:
            print("You cant go there, go again.")

    board[position] = player

    display_board()

def check_is_game_over():
    check_for_winner()
    check_if_tie()
    return

def check_for_winner():
    global winner
    row_winner=check_rows()

    col_winner=check_columns()

    dia_winner=check_dia()


    if row_winner:
        winner=row_winner

    if col_winner:
        winner=col_winner

    if dia_winner:
        winner=dia_winner

    return

def check_rows():
    global game_still_going
    row_1= board[0]==board[1]==board[2] != "-"
    row_2= board[3]==board[4]==board[5] != "-"
    row_3= board[6]==board[7]==board[8] != "-"
    if row_1 or row_2 or row_3:
        game_still_going=False

    if row_1:
        return board[0]
    if row_2:
        return board[3]
    if row_3:
        return board[6]
    return

def check_columns():
    global game_still_going
    col_1= board[0]==board[3]==board[6] != "-"
    col_2= board[1]==board[4]==board[7] != "-"
    col_3= board[2]==board[5]==board[8] != "-"
    if col_1 or col_2 or col_3:
        game_still_going=False

    if col_1:
        return board[0]
    if col_2:
        return board[1]
    if col_3:
        return board[2]
    return

def check_dia():
    dia_1= board[0]==board[4]==board[8] != "-"
    dia_2= board[2]==board[4]==board[6] != "-"
    if dia_1 or dia_2:
        game_still_going=False

    if dia_1:
        return board[0]
    if dia_2:
        return board[2]
    return


def check_if_tie():
    global game_still_going
    if "-" not in board:
        game_still_going = False
    return

def flip_player():
    global current_player
    if current_player=="X":
        current_player="O"
    else:
        current_player="X"
    return
play_game()
