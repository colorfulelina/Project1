# Project1
import random

#symbols for slot machine
symbols = ["!", "@", "#", "$", "%"]

#global variables
spin_list = []
bank = 500
amount = 0

#randomly assigning 3 random symbols from the list symbols to 3 variables : s1, s2, s3
def spin_wheel():
  s_list =[]
  s1 = random.choice(symbols)
  s2 = random.choice(symbols)
  s3 = random.choice(symbols) 
  s_list.append(s1)
  s_list.append(s2)
  s_list.append(s3)
  return s_list

"""
once assigned, based on the pattern of the 3 variables, it will add, decrease, or do nothing to the amount of money in your bank. if 3 of them are the same, it will double the amount, if 3 of them are different, it will decrease the amount and if two of them are the same, your bank money stays the same
"""
def determine_outcome(s):
  global bank, amount
  s1 = s[0]
  s2 = s[1]
  s3 = s[2]
  if s1 == s2 == s3:
    print ("You WIN")
    bank = bank +(2*amount)
  else:
    if s1 == s2:
      print("The result is Draw")
    if s2 == s3:
      print("The result is Draw")
    if s1 == s3:
      print("The result is Draw")
  if s1 != s2 and s1 != s3 and s2 != s3:
      print("You LOSE")
      bank = bank - amount
    
#check user input to make sure it is valid
def check_user_input(input):
  global amount
  try:
    amount = int(input)
    return True
  except ValueError:
    print("invalid input. try again")
    return False


print("Welcome to my Casino")

"""
this the main loop that has all the functions. It takes the amount of money that user wants to spend and puts it in the slot machine. It also takes care if user bets too much, or if user becomes bankrupt.
"""
while True:
  print()
  print("You have " + "$" + str(bank) + " in the bank")
  user_input = input("How much do you want to bet? press q to quit: ")
  if user_input == "q":
   break
  if check_user_input(user_input) == False:
    continue

  
  if bank == 0:
    print("You don't have anymore money. go home we're kicking you out" )
    break
  if amount > bank:
    print ("You don't have this much money, bet again with a smaller amount")
    continue
  
  spin_list = spin_wheel()
 
  print(spin_list)
  determine_outcome(spin_list)
  
