# python_projects
import random as rn
import emoji as em
winner=0
# variable hold the winner according to dice total : (if >= 50) winner declare using this variable

c_dice,u_dice=0,0
# dive variable hold the random value from random module and it's overwrite turn by turn 

user_dice_total,computer_dice_total=0,0  
# variable can hold dice total of user and computer bcz we have to increase and decrese according to snack bit or change poistion on board 

c_pos,u_pos=0,0
# variable can hold the position of user and computer 

l,Choice=[],[] 
# l is empty list for making dash board 
# choice is empty list for 

i,j=0,0
# this hold the position of snake_bite according to dice_total of both player

snake_bit_at=[14,20,22,49]
# snake_bit have predefined snake_bit 

step_back=[5,17,4,24]
# according to snake_bit number take action to step back to decrease total_dice value of player who snake bitten

# user have choice to choose sign  
Choice.append(em.emojize(':snake:'))
Choice.append("\U0001f7e1")
Choice.append("\U0001f7e5")
Choice.append("\U0001f7e8")
ch=int(input(f"Enter your Sign : {Choice}\n"))
if ch==1:
    c1=Choice[0]
elif ch==2:
    c1=Choice[1]
elif ch==3:
    c1=Choice[2]
else:
    c1=Choice[3]

# dashboard making function 1 to 50 append in empty list 
def make_dash_board():
    for i in range(1,51):
        l.append(i)
    l[13]='\U0001f534'
    l[19]='\U0001f534'
    l[21]='\U0001f534'
    l[48]='\U0001f534'
make_dash_board()

# Game starting condition 
if (input("Yes to start Game: ")) == "yes":
    # Game in infinite loop until this not get winner 
    while 1:
        if ((winner!= "USER") or (winner!= "COMPUTER")):  # Game stoping condition
            if (input("\nYOUR TURN y/n: ")) == 'y':  # Game quit condition
                print(f"USER TURN : ")
                u_dice = rn.randint(1,6) # dice role
                print(f"USER Dice = {u_dice}") 
                user_dice_total+=u_dice    # to move in dashboart 
                if user_dice_total >=50:    # condition of winner
                    winner = "USER"
                    print("---------------------------------------------------")
                    print(f"| CONGRATULATION !! winner {winner} \n Well played |")
                    print("---------------------------------------------------")
                    exit(0)

                u_pos=l[user_dice_total-1] # hold position of user
                l[user_dice_total-1]= c1  # replace dashboard number with your sign in first step

                if user_dice_total in snake_bit_at:  # snake_bit condtion if dice_total on snake_bit
                    i=user_dice_total  # to print where snake bitten
                    print("\n------------------------")
                    print(f"| USER SNAKE BIT AT {i} |")
                    print("------------------------")
                    snake_bite_u=1    
                    if i==14: 
                        l[13]='\U0001f534'          # change the position according to snakebit if this value overwrite by user sign , on snake bit need to step back so sign can over write by red spot again
                        user_dice_total-=5          # decrese dice according to step back
                        i=user_dice_total
                        u_pos=l[user_dice_total-1]  # hold the user old position to safe from re over write by user sign
                        l[user_dice_total-1]= c1    # and final replace step back position to user sign
                    elif i==20:                     # other things same here bellow
                        l[19]='\U0001f534'
                        user_dice_total-=3
                        i=user_dice_total
                        u_pos=l[user_dice_total-1]
                        l[user_dice_total-1]= c1
                    elif i==22:
                        l[21]='\U0001f534'
                        user_dice_total-=4
                        i=user_dice_total
                        u_pos=l[user_dice_total-1]
                        l[user_dice_total-1]= c1
                    elif i==49:
                        l[48]='\U0001f534'
                        user_dice_total-=24
                        i=user_dice_total
                        u_pos=l[user_dice_total-1]
                        l[user_dice_total-1]= c1
                else:
                    snake_bite_u=0 
                    
                # computer turn starting   
                    
                print(f"COMPUTER TURN : ")
                c_dice = rn.randint(1,6)   # computer dice role
                print(f"COMPUTER Dice = {c_dice}")
                computer_dice_total+=c_dice   # change position according to total_dice of computer
                if computer_dice_total >=50:           # condition of winner
                    winner="COMPUTER"
                    print("------------------------------------------------------")
                    print(f"| Better luck next time {winner}(AI) Beat you hhaha! |")
                    print("------------------------------------------------------")
                    exit(0)

                c_pos=l[computer_dice_total-1]   # hold the position of computer turn
                l[computer_dice_total-1]= em.emojize(':laptop:')  # default set (laptop) sign using emoji module 
                        
                if computer_dice_total in snake_bit_at:   # condition for comoputer snake bit
                    j=computer_dice_total  # to print where snake bitten 
                    print("---------------------------")
                    print(f"| COMPUTER SNAKE BIT AT {j} |")
                    print("---------------------------")
                    snake_bite_c=1 
                    if j==14:
                        l[13]='\U0001f534'                                # same thing here as user snake bit and go back with step back number
                        computer_dice_total-=5
                        j = computer_dice_total
                        c_pos=l[computer_dice_total-1]
                        l[computer_dice_total-1]= em.emojize(':laptop:') # replace step back with laptop sign
                    elif j==20:                                            # other same things below 
                        l[19]='\U0001f534'
                        computer_dice_total-=3
                        j = computer_dice_total
                        c_pos=l[computer_dice_total-1]
                        l[computer_dice_total-1]= em.emojize(':laptop:')
                    elif j==22:
                        l[21]='\U0001f534'
                        computer_dice_total-=4
                        j = computer_dice_total
                        c_pos=l[computer_dice_total-1]
                        l[computer_dice_total-1]= em.emojize(':laptop:')
                    elif j==49:
                        l[48]='\U0001f534'
                        computer_dice_total-=24
                        j = computer_dice_total
                        c_pos=l[computer_dice_total-1]
                        l[computer_dice_total-1]= em.emojize(':laptop:')
                else:
                    snake_bite_c=0
                    
                # to check user and computer sign at one position 
                # if same : to hold this position to temp variable than rewrite this user/computer position  
                if user_dice_total == computer_dice_total:
                    u_temp=user_dice_total
                    c_temp=computer_dice_total
                    count=1
                else:
                    count=0
    
                print(f"|---------------------------------------------------|")
                print(f"  {l[40]}   {l[41]}   {l[42]}   {l[43]}   {l[44]}   {l[45]}   {l[46]}   {l[47]}   {l[48]}   {l[49]}")
                print(f"|---------------------------------------------------|")
                print(f"  {l[39]}   {l[38]}   {l[37]}   {l[36]}   {l[35]}   {l[34]}   {l[33]}   {l[32]}   {l[31]}   {l[30]}")
                print(f"|---------------------------------------------------|")
                print(f"  {l[20]}   {l[21]}   {l[22]}   {l[23]}   {l[24]}   {l[25]}   {l[26]}   {l[27]}   {l[28]}   {l[29]}")  
                print(f"|---------------------------------------------------|")
                print(f"  {l[19]}   {l[18]}   {l[17]}   {l[16]}   {l[15]}   {l[14]}   {l[13]}   {l[12]}   {l[11]}   {l[10]}")
                print(f"|---------------------------------------------------|")
                print(f"  {l[0]}    {l[1]}    {l[2]}    {l[3]}    {l[4]}    {l[5]}    {l[6]}    {l[7]}    {l[8]}   {l[9]}")
                print(f"|---------------------------------------------------|")
                print(f"USER ON : {user_dice_total}")
                print(f"COMPUTER ON : {computer_dice_total}")
                if snake_bite_u == 1:
                    print(f"USER GO BACK TO {i}")
                else:
                    snake_bite_u =0
                if snake_bite_c == 1:
                    print(f"COMPUTER GO BACK TO {j}")
                else:
                    snake_bite_c =0
                if count!=1:
                    l[user_dice_total-1]=u_pos   
                    l[computer_dice_total-1]=c_pos
                # it's all about replace sign with number and change position
                # old position replace with sign : we need to assign this value with number again
                # count is need for print after next move so we require to print this dash board first after backend work this change old position with number 
                else:
                    l[user_dice_total-1]=u_temp  # on list position assinged by number which hold by u_temp variable
                    l[computer_dice_total-1]=c_temp  # on list position assinged by number which hold by c_temp variable
            
            # when use want to exit this condition work when user input not equal to 'y'
            else:
                print("You Exit Game Better Luck Next Time")
                exit(0)


