# Battleship
my Game


from random import randint

board = []

for x in range(0, 5):
  board.append(["+"] * 5)

#Prints out board  
def print_board(board):
  for row in board:
    print " ".join(row)
  print "\n"
 
#gives random return within scopes of a square matrice
def random_num(board):
  return randint(0, len(board) - 1)

ship_row = random_num(board)
ship_col = random_num(board)


#runs through the collection of a players guess for a single turn
#returns int 1, 2, or 3
#displays error for incorrect input
def run_turn(turn):  
  guess_row = int(raw_input("Guess Row: ")) - 1
  guess_col = int(raw_input("Guess Col: ")) - 1

  if guess_row == ship_row and guess_col == ship_col:
    return 1
  else:
    if guess_row not in range(5) or \
      guess_col not in range(5):
      print "Oops, that's not even in the ocean."
      print "Try Again"
      return 2
    elif board[guess_row][guess_col] == "X":
      print( "You guessed that one already." )
      print "Try Again"
      return 2
    else:
      board[guess_row][guess_col] = "X"
      return 3

def run_game(y):
  for x in range(y):
    if x == 0:
      print "\n" *30
      print "Turn 1 \n"
      print_board(board)
    determine = run_turn(x)
    if determine == 1:
      board[ship_row][ship_col] = "O"
      print "\n" *30
      print "Congratulations! You sank my battleship!"
      print "%s tries out of %s" % (x + 1, y)
      print "YOU'RE A CHAMPION\n"
      print_board(board)
      print "Game Over"
      break
    while determine == 2:
      determine = run_turn(x)  
    if x == y-1 and determine == 3:
      board[ship_row][ship_col] = "O"
      print "\n" *30
      print "YOU'RE A LOSER\n"
      print_board(board)
      print "Game Over"
      break
    print "\n" *30
    print "You missed my battleship!\n"
    print "Turn %s\n" % (x+2)
    print_board(board)

    
def difficulty():
  print "\nYou can choose your difficulty"
  print "\nIf you pick easy you will have 15 turns"
  print "medium will give you 10 turns, and hard 5 turns."
  dif_of_game = raw_input("\nWould you like easy, medium, or hard?")
  for x in range(2):
    if dif_of_game == "easy":
      run_game(15)
      break
    elif dif_of_game == "medium":
      run_game(10)
      break
    elif dif_of_game == "hard":
      run_game(5)
      break
    elif x == 1:
      print "\nYou must be slow...We'll go easy"
      raw_input()
      run_game(15)
    else:
      print "\nLet's pick one of the options....okay?"
      dif_of_game = raw_input("\nWould you like easy, medium, or hard?\n")
    
def instructions():
  print "\nIt is your mission to sink my ship"
  print "You have 4 turns to do so\n"
  
  
def accept():
  instructions()
  yayornay = raw_input("Do you accept?\n")
  if yayornay == "yes":
    difficulty()
  else:
    print"\nAre you slow?\nDo you need the instructions again?"
    if raw_input() == "yes":
      instructions()
      if raw_input("Are you ready now?\n") == "yes":
        difficulty()
      else:
        print "\nProbably never will be....Idiot"
    else:
      if raw_input("\nAre you ready then?\n") == "yes":
        difficulty()
      else:
        print "\nProbably never will be....Idiot"
        

print "This is the game of \n   BATTLESHIP"
accept()
