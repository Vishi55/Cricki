from random import randint
runs = 0
com_runs = 0
toss = 0
print("Welcome to Hand Cricket! Like in real cricket, you have to chase/defend the score. In order, to be out or get the computer out you will have to play the same number as the computer. ")

def game_toss():
    global toss
    print("Your number and the computer's number will be added. Chose between 1 to 6")
    player_toss = int(input("Chose a number. If it is even you win the toss!"))
    if player_toss > 6:
        print("Remember, you can only chose numbers 1 - 6!")
        main()
    com_toss = randint(1,6)
    print("Computer has chosen", com_toss)
    toss = player_toss + com_toss
    if toss == 2 or toss == 4 or toss == 6 or toss == 8 or toss == 10 or toss == 12:
        chose = str(input("You have won the toss. What will you do now? Bat/Ball"))
        if chose == 'Bat':
            print("You have chosen to bat... GAME STARTING!")
            bat_first()
        else:
            print("You have chose to bowl... GAME STARTING!")
            bowl_first()
    else:
        bat_ball = randint(1,2)
        if bat_ball == 1:
            print("The Computer has chosen to bat first! GAME STARTING!")
            bowl_first()
        elif bat_ball == 2:
            print("The Computer has chosen to ball first! GAME STARTING!")
            bat_first()
        else:
            print("There is a flaw in the coin.You have been asked to bat first. GAME STARTING! ")
            bat_first()

def bat_first():
    global runs
    print("You will have to bat now, chose an number between 1 to 6.")
    print("Chosing a number higher than 6 is illegal and you will be sent back!")
    print("If you chose a an number the same as the computer you will be out!")
    while True:
        com_number = randint(1,6)
        number = int(input("What is your number?"))
        runs += number
        if com_number == number or number > 6:
            print("The Computer has chosen",com_number,"!")
            print("You have GOT OUT! You have scored,", runs - number,"runs.")
            runs = runs - number
            print("You will have to bowl now.")
            bowl_second()
            break
        if runs > 50:
            print("A fine knock- you can see the batsmen is in form here.")
        elif runs > 100:
            print("This batsmen is exceptional. A innings to remember.")
        else:
            print("The Computer has chosen", com_number)
            print("So far you have scored", runs,"runs")

def bowl_first():
   global com_runs
   print("To get the computer out chose the same number as the computer!")
   while True:
        com_number = randint(1,6)
        number = int(input("What is your number?"))
        com_runs += com_number
        print("The Computer has chosen", com_number)
        if com_number == number:
            print("You have got the Computer out!")
            com_runs = com_runs - number
            bat_second()
        elif com_runs < 0:
          com_runs = 0
            
          print("Computer has scored",com_runs-number, "runs.")
          bat_second()
  
          break
        else:
            print("So far the Computer has scored", com_runs,"runs.")


def bat_second():
    global runs
    print("You will have to bat now. To win you need..",com_runs, "runs.")
    print("Chose an number between 1 to 6.")
    print("If you chose a an number the same as the computer you will be out!")
    while True:
        com_number = randint(1,6)
        number = int(input("What is your number?"))
        runs += number
        if runs > com_runs:
            print("The Computer has chosen",com_number,".")
            print("You have scored", runs)
            print("Well done what a amazing win, you beat the computer.")
            end()
        if com_number == number or number > 6:
            print("The computer has chosen",com_number,"!")
            print("You have got OUT! You have scored",runs - number)
            runs = runs - number
            if runs < com_runs:
                print("Unlucky, the computer has beaten you by",com_runs - runs , "runs.")
                end()
                break
            if runs > 50:
                print("What a fabulous innings!")
            elif runs > 100:
                print("This is a true talent.  A marvellous innings.")
        else:
            print("The Computer has chosen", com_number,".")
            print("So far you have scored",runs,"runs.")

def bowl_second():
    global com_runs
    print("To get the computer out chose the same number as the computer!")
    while True:
        com_number = randint(1, 6)
        number = int(input("What is your number?"))
        com_runs += com_number
        if com_runs > runs:
            print("The Computer is at",com_runs, '!')
            print("That was a close one... The Computer has beaten you!")
            end()
            break
        elif com_number == number and com_runs < runs:
            print("The computer chose",com_number,"!")
            print("Well done, what a great win! You have won by", runs - com_runs, "runs.")
            end()
            break
        else:
            print("The Computer has chosen",com_number)
            print("The Computer has scored", com_runs, "runs")

def main():
        print("Let's start the toss!")
        game_toss()


def end():
        answer = input(("Would you like a rematch? (Y/N)"))
        if answer == "Y":
            print("Ok! Let's do the toss!")
            game_toss()
        if answer == "N":
          print("Thanks for playing! You were an excellent cricketer!")

main()
