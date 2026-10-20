import random
import math
import time

#--------------------COLOR CODES--------------------
reset="\033[0m"
red="\033[91m"
green="\033[92m"
yellow="\033[93m"
blue="\033[94m"
cyan="\033[96m"
magenta="\033[95m"

#------------------------------------------INTRO------------------------------------------
def intro():
    print(cyan+"\nENTERING SERIFFY..."+reset)
    time.sleep(2)
    print(yellow+"-"*80+reset)
    print(magenta+" ✨ SERIFFY ✨"+reset)
    print(blue+" Your Personal Study Assistant"+reset)
    time.sleep(1)

#------------------------------------------TO-DO LIST (WITH FILE HANDLING)------------------------------------------
def load_tasks():
    """Helper function to load tasks from a text file when the app starts"""
    tasks=[]
    try:
        # 'r' opens the file in read mode
        with open("tasks.txt","r") as file:
            for line in file:
                tasks.append(line.strip()) # strip() removes extra newline spaces
    except FileNotFoundError:
        # If the file doesn't exist yet, just return an empty list safely
        pass
    return tasks

def save_tasks(tasks):
    """Helper function to permanently save tasks to a text file"""
    # 'w' opens the file in write mode, overwriting old data with the updated list
    with open("tasks.txt","w") as file:
        for task in tasks:
            file.write(task+"\n")

def to_do_list():
    while True:
        # Dynamically load the saved tasks from the text file every time the menu opens
        tasks_list=load_tasks()
        
        print(red+"\n✨ TO-DO LIST (Saved Tracking) ✨"+reset)
        print(yellow,"1. Add task",reset)
        print(yellow,"2. View tasks",reset)
        print(yellow,"3. Delete task",reset)
        print(yellow,"4. Exit",reset)
        choice1=input("Choose: ")

        if choice1=="1":
            task_item=input("Enter task: ")
            tasks_list.append(task_item)
            save_tasks(tasks_list) # Save to text file immediately
            print(green+"Task added and saved successfully!"+reset)

        elif choice1=="2":
            if len(tasks_list)==0:
                print(red+"No tasks found in tasks.txt!"+reset)
            else:
                print(cyan+"\n--- Your Saved Tasks ---"+reset)
                for idx1,task_item in enumerate(tasks_list,start=1):
                    print(idx1,".",task_item)

        elif choice1=="3":
            if len(tasks_list)==0:
                print(red+"No tasks to delete!"+reset)
            else:
                for idx2,task_item in enumerate(tasks_list,start=1):
                    print(idx2,".",task_item)
                try:
                    deleting_task_number=int(input("Enter the task number to delete: "))
                    if 1<=deleting_task_number<=len(tasks_list):
                        tasks_list.pop(deleting_task_number-1)
                        save_tasks(tasks_list) # Update text file after deletion
                        print(green+"Task deleted and storage updated!"+reset)
                    else:
                        print(red+"Invalid task number!"+reset)
                except ValueError:
                    print(red+"Please enter a valid number!"+reset)

        elif choice1=="4":
            print(blue,"Exiting To-Do List...",reset)
            break
        else:
            print(red+"Invalid choice! Enter 1-4."+reset)

#-----------------------------------------PERCENTAGE CALCULATOR-----------------------------------------
def percentage_calculator():
    n=int(input("Number of subjects: "))
    total_marks=0
    obtained_marks=0
    for i in range(n):
        marks=float(input(f"Total marks for subject {i+1}: "))
        obtained=float(input(f"Obtained marks for subject {i+1}: "))
        total_marks+=marks
        obtained_marks+=obtained
    if total_marks==0:
        print(red+"Total marks cannot be zero!"+reset)
        return
    percentage=(obtained_marks/total_marks)*100
    print(green,"Percentage:",percentage,reset)

#-----------------------------------------STOPWATCH-----------------------------------------
def stopwatch():
    voi=input("Do you want to start/end? ").lower()
    if voi=="start":
        print(red,"✨ Starting STOPWATCH ✨",reset)
        time.sleep(1)
        minutes=int(input("Enter minutes: "))
        total_seconds=minutes*60
        print(cyan,"Stopwatch started!",reset)
        while total_seconds>=0:
            mins=total_seconds//60
            secs=total_seconds%60
            print(magenta,f"{mins}:{secs}",reset)
            time.sleep(1)
            total_seconds-=1
        print(red,"Time's up!",reset)
    else:
        print(blue,"Exiting stopwatch...",reset)
        return

#----------------------------------------FORTUNE COOKIE-----------------------------------------
def fortune_cookie():
    while True:
        voi=input("Do you want to start/end? ").lower()
        if voi=="start":
            quotes=[
                "Small steps every day lead to big success.",
                "Discipline is choosing what you want most.",
                "Your future is created by what you do today.",
                "Focus now, shine later.",
                "Hard work beats talent when talent doesn't work.",
            ]
            print(red+"✨ Opening fortune cookie..."+reset)
            time.sleep(2)
            print(green+random.choice(quotes)+reset)
        elif voi=="end":
            print(blue,"Exiting fortune cookie...",reset)
            return
        else:
            print(red+"Invalid choice! Type 'start' or 'end'."+reset)

#--------------------------------------------CALCULATOR---------------------------------------------
def calculator():
    print(magenta+"✨ CALCULATOR"+reset)
    print(yellow+"1. Add\n2. Subtract\n3. Multiply\n4. Divide"+reset)
    choice=input("Choose: ")
    n=int(input("How many numbers? "))
    numbers=[float(input(f"Enter number {i+1}: ")) for i in range(n)]

    if choice=="1":
        result=sum(numbers)
    elif choice=="2":
        result=numbers[0]
        for num in numbers[1:]:
            result-=num
    elif choice=="3":
        result=1
        for num in numbers:
            result*=num
    elif choice=="4":
        if 0 in numbers[1:]:
            print(red+"Error: Division by zero!"+reset)
            return
        result=numbers[0]
        for num in numbers[1:]:
            result/=num
    else:
        print(red+"Invalid choice!"+reset)
        return
    print(green,"Result:",result,reset)

#----------------------------------------UNIT CONVERTER-----------------------------------------
def converter():
    print(magenta,"✨ UNIT CONVERTER ✨",reset)
    print(yellow+"\n1. Km to Miles\n2. Miles to Km\n3. Celsius to Fahrenheit\n4. Fahrenheit to Celsius\n5. Kg to Pounds\n6. Pounds to Kg"+reset)
    c=input("Enter choice: ")
    x=float(input("Enter number: "))
    if c=="1":
        y=x*0.621
        print(green,x,"km =",y,"miles",reset)
    elif c=="2":
        y=x/0.621
        print(green,x,"miles =",y,"km",reset)
    elif c=="3":
        y=(x*9/5)+32
        print(green,x,"°C =",y,"°F",reset)
    elif c=="4":
        y=(x-32)*5/9
        print(green,x,"°F =",y,"°C",reset)
    elif c=="5":
        y=x*2.205
        print(green,x,"kg =",y,"pounds",reset)
    elif c=="6":
        y=x/2.205
        print(green,x,"pounds =",y,"kg",reset)
    else:
        print(red+"Invalid choice!"+reset)

#----------------------------------------POMODORO TIMER-----------------------------------------
def pomodoro():
    answer=input("Start pomodoro? (y/n): ").lower()
    if answer=="y":
        work_minutes=int(input("Enter work minutes: "))
        break_minutes=int(input("Enter break minutes: "))
        print(cyan,"Work started!",reset)
        time.sleep(work_minutes*60)
        print(cyan,"Break started!",reset)
        time.sleep(break_minutes*60)
        print(green,"Pomodoro session finished!",reset)
    else:
        print(red,"Pomodoro not started.",reset)

#----------------------------------------MATH SOLVER-----------------------------------------
def math_solver():
    c=""
    while c!="7":
        print(cyan+"✨ MATH SOLVER ✨"+reset)
        print(yellow+"1. Square Root"+reset)
        print(yellow+"2. Power"+reset)
        print(yellow+"3. Factorial"+reset)
        print(yellow+"4. Trigonometry"+reset)
        print(yellow+"5. Log base 10"+reset)
        print(yellow+"6. Ceiling and Floor"+reset)
        print(yellow+"7. Exit"+reset)
        c=input("Enter choice: ")
        if c=="1":
            n=float(input("Enter number: "))
            print(green,"Square root:",math.sqrt(n),reset)
        elif c=="2":
            a=float(input("Enter base: "))
            b=float(input("Enter power: "))
            print(green,"Result:",math.pow(a,b),reset)
        elif c=="3":
            n=int(input("Enter number: "))
            print(green,"Factorial:",math.factorial(n),reset)
        elif c=="4":
            r=float(input("Enter angle in radians: "))
            print(green,"sin =",math.sin(r),reset)
            print(green,"cos =",math.cos(r),reset)
            print(green,"tan =",math.tan(r),reset)
        elif c=="5":
            n=float(input("Enter number: "))
            print(green,"Log base 10:",math.log10(n),reset)
        elif c=="6":
            n=float(input("Enter number: "))
            print(green,"Ceil =",math.ceil(n),"| Floor =",math.floor(n),reset)
        elif c=="7":
            print(blue,"Exiting Math Solver...",reset)
            break
        else:
            print(red+"Invalid choice!"+reset)

#----------------------------------------GEOMETRY SOLVER-----------------------------------------
def geometry_solver():
    print(magenta+"\n✨ GEOMETRY SOLVER ✨"+reset)
    print(yellow+"1. Area of Square\n2. Area of Rectangle\n3. Area of Circle\n4. Volume of Cube\n5. Volume of Cylinder\n6. Exit"+reset)
    choice=input("Choose: ")
    if choice=="1":
        side=float(input("Enter side: "))
        print(green,"Area =",side2,reset)
    elif choice=="2":
        l=float(input("Enter length: "))
        w=float(input("Enter width: "))
     print(green,"Area =",lw,reset)
      elif choice == "3": 
            r = float(input("Enter radius: ")) 
            print(green, "Area =", math.pi * (r ** 2), reset) 
        elif choice == "4": 
            side = float(input("Enter side: ")) 
            print(green, "Volume =", side ** 3, reset) 
        elif choice == "5": 
            r = float(input("Enter radius: ")) 
            h = float(input("Enter height: ")) 
            print(green, "Volume =", math.pi * (r ** 2) * h, reset) 
        elif choice == "6": 
            print(blue + "Exiting geometry solver..." + reset) 
            return

#----------------------------------------PHYSICS LIBRARY----------------------------------------- 
def physics_library(): 
    print(cyan + "\n✨ PHYSICS LIBRARY ✨" + reset) 
    physics_dict = {
        "acceleration": "Rate of change of velocity",
        "amplitude": "Maximum displacement of a wave",
        "angle": "Measure of rotation between two lines",
        "atom": "Smallest unit of a chemical element", 
        "charge": "Property causing electromagnetic interaction", 
        "current": "Flow of electric charge", 
        "density": "Mass per unit volume" 
    } 
    word = input("Enter a physics term to look up: ").strip().lower() 
    if word in physics_dict: 
        print(green + physics_dict[word] + reset) 
    else: 
        print(red + "Term not found!" + reset) 

#----------------------------------------MAIN MENU ENGINE----------------------------------------- 
def main_menu(): 
    intro() 
    while True: 
        print(cyan + "\n================ MAIN MENU ================" + reset) 
        print("1. To-Do List          2. Percentage Calculator") 
        print("3. Stopwatch          4. Fortune Cookie") 
        print("5. Calculator          6. Unit Converter") 
        print("7. Pomodoro Timer      8. Math Solver") 
        print("9. Geometry Solver     10. Physics Library") 
        print("11. Exit Program") 
        print(cyan + "===========================================" + reset) 
        
main_choice = input("Choose an option (1-11): ").strip() 
        
if main_choice == "1": 
            to_do_list() 
        elif main_choice == "2": 
            percentage_calculator() 
        elif main_choice == "3": 
            stopwatch() 
        elif main_choice == "4": 
            fortune_cookie() 
        elif main_choice == "5": 
            calculator() 
        elif main_choice == "6": 
            converter() 
        elif main_choice == "7": 
            pomodoro() 
        elif main_choice == "8": 
            math_solver() 
        elif main_choice == "9": 
            geometry_solver() 
        elif main_choice == "10": 
            physics_library() 
        elif main_choice == "11": 
            print(magenta + "\nGoodbye Aisha! Good luck studying." + reset) 
            break 
        else: 
            print(red + "Invalid choice! Enter a number between 1 and 11." + reset) 

if __name__ == "__main__":
    main_menu()
