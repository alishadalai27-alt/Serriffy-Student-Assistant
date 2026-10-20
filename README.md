import random
import math
import time
import sys

#--------------------COLOR CODES--------------------
reset="\033[0m"
red="\033[91m"
green="\033[92m"
yellow="\033[93"
blue="\033[94m"
cyan="\033[96m"
magenta="\033[95m"

#------------------------------------------INTRO------------------------------------------
def intro():
    print(cyan + "\nENTERING SERIFFY..." + reset)
    time.sleep(1)
    print(yellow + "-"*80 + reset)
    print(magenta + " ✨ SERIFFY ✨" + reset)
    print(blue + " Your Personal Study Assistant" + reset)
    time.sleep(1)

#------------------------------------------TO-DO LIST------------------------------------------
def to_do_list():
    tasks_list = []
    while True:
        print(red + "\n✨ TO-DO LIST ✨" + reset)
        print(yellow + "1. Add task" + reset)
        print(yellow + "2. View tasks" + reset)
        print(yellow + "3. Delete task" + reset)
        print(yellow + "4. Exit" + reset)
        choice1 = input("Choose: ").strip()
        
        if choice1 == "1":
            task_item = input("Enter task: ").strip()
            if task_item:
                tasks_list.append(task_item)
                print(green + "Task added successfully!" + reset)
            else:
                print(red + "Task cannot be empty!" + reset)
        elif choice1 == "2":
            if len(tasks_list) == 0:
                print(red + "No tasks found!" + reset)
            else:
                for idx1, task_item in enumerate(tasks_list, start=1):
                    print(f"{idx1}. {task_item}")
        elif choice1 == "3":
            if len(tasks_list) == 0:
                print(red + "No tasks to delete!" + reset)
            else:
                for idx2, task_item in enumerate(tasks_list, start=1):
                    print(f"{idx2}. {task_item}")
                try:
                    deleting_task_number = int(input("Enter the task number to delete: "))
                    if 1 <= deleting_task_number <= len(tasks_list):
                        tasks_list.pop(deleting_task_number - 1)
                        print(green + "Task deleted successfully!" + reset)
                    else:
                        print(red + "Invalid task number!" + reset)
                except ValueError:
                    print(red + "Please enter a valid number!" + reset)
        elif choice1 == "4":
            print(blue + "Exiting To-Do List..." + reset)
            break
        else:
            print(red + "Invalid choice! Enter 1-4." + reset)

#-----------------------------------------PERCENTAGE CALCULATOR-----------------------------------------
def percentage_calculator():
    try:
        n = int(input("Number of subjects: "))
        total_marks = 0
        obtained_marks = 0
        for i in range(n):
            marks = float(input(f"Total marks for subject {i+1}: "))
            obtained = float(input(f"Obtained marks for subject {i+1}: "))
            total_marks += marks
            obtained_marks += obtained
        
        if total_marks > 0:
            percentage = (obtained_marks / total_marks) * 100
            print(green, f"Percentage: {percentage:.2f}%", reset)
        else:
            print(red + "Total marks cannot be zero!" + reset)
    except ValueError:
        print(red + "Invalid numeric input!" + reset)

#-----------------------------------------COUNTDOWN TIMER (STOPWATCH)-----------------------------------------
def stopwatch():
    voi = input("Do you want to start/end? ").lower().strip()
    if voi == "start":
        print(red, "✨ Starting COUNTDOWN TIMER ✨", reset)
        time.sleep(1)
        try:
            minutes = int(input("Enter minutes: "))
            total_seconds = minutes * 60
            print(cyan, "Timer started!", reset)
            
            while total_seconds >= 0:
                mins = total_seconds // 60
                secs = total_seconds % 60
                sys.stdout.write(magenta + f"\rTime remaining: {mins:02d}:{secs:02d}" + reset)
                sys.stdout.flush()
                time.sleep(1)
                total_seconds -= 1
            print(red + "\nTime's up!" + reset)
        except ValueError:
            print(red + "Please enter a valid integer for minutes!" + reset)
    else:
        print(blue + "Exiting timer..." + reset)

#----------------------------------------FORTUNE COOKIE-----------------------------------------
def fortune_cookie():
    quotes = [
        "Small steps every day lead to big success.",
        "Discipline is choosing what you want most.",
        "Your future is created by what you do today.",
        "Focus now, shine later.",
        "Hard work beats talent when talent doesn't work.",
    ]
    while True:
        voi = input("Do you want to start/end? ").lower().strip()
        if voi == "start":
            print(red + "✨ Opening fortune cookie..." + reset)
            time.sleep(1)
            print(green + random.choice(quotes) + reset)
        elif voi == "end":
            print(blue + "Exiting fortune cookie..." + reset)
            break
        else:
            print(red + "Invalid choice! Type 'start' or 'end'." + reset)

#--------------------------------------------CALCULATOR---------------------------------------------
def calculator():
    print(magenta + "✨ CALCULATOR" + reset)
    print(yellow + "1. Add\n2. Subtract\n3. Multiply\n4. Divide" + reset)
    choice = input("Choose: ").strip()
    if choice not in ["1", "2", "3", "4"]:
        print(red + "Invalid choice!" + reset)
        return
        
    try:
        n = int(input("How many numbers? "))
        numbers = [float(input(f"Enter number {i+1}: ")) for i in range(n)]
        
        if choice == "1":
            result = sum(numbers)
        elif choice == "2":
            result = numbers
            for num in numbers[1:]:
                result -= num
        elif choice == "3":
            result = 1
            for num in numbers:
                result *= num
        elif choice == "4":
            if 0 in numbers[1:]:
                print(red + "Error: Division by zero!" + reset)
                return
            result = numbers
            for num in numbers[1:]:
                result /= num
                
        print(green, "Result:", result, reset)
    except (ValueError, IndexError):
        print(red + "Invalid input data, calculation failed." + reset)

#----------------------------------------UNIT CONVERTER-----------------------------------------
def converter():
    print(magenta, "✨ UNIT CONVERTER ✨", reset)
    print(yellow + "\n1. Km to Miles\n2. Miles to Km\n3. Celsius to Fahrenheit\n4. Fahrenheit to Celsius\n5. Kg to Pounds\n6. Pounds to Kg" + reset)
    c = input("Enter choice: ").strip()
    try:
        x = float(input("Enter number: "))
        if c == "1":
            print(green, f"{x} km = {x * 0.621:.3f} miles", reset)
        elif c == "2":
            print(green, f"{x} miles = {x / 0.621:.3f} km", reset)
        elif c == "3":
            print(green, f"{x} °C = {(x*9/5)+32:.2f} °F", reset)
        elif c == "4":
            print(green, f"{x} °F = {(x-32)*5/9:.2f} °C", reset)
        elif c == "5":
            print(green, f"{x} kg = {x*2.205:.3f} pounds", reset)
        elif c == "6":
            print(green, f"{x} pounds = {x/2.205:.3f} kg", reset)
        else:
            print(red + "Invalid choice!" + reset)
    except ValueError:
        print(red + "Please enter a valid numeric value!" + reset)

#----------------------------------------POMODORO TIMER-----------------------------------------
def pomodoro():
    answer = input("Start pomodoro? (y/n): ").lower().strip()
    if answer == "y":
        try:
            work_minutes = int(input("Enter work minutes: "))
            break_minutes = int(input("Enter break minutes: "))
            
            print(cyan + "\n💼 Work session started!" + reset)
            for remaining in range(work_minutes * 60, 0, -1):
                sys.stdout.write(magenta + f"\rWork Time left: {remaining // 60:02d}:{remaining % 60:02d}" + reset)
                sys.stdout.flush()
                time.sleep(1)
                
            print(cyan + "\n☕ Break session started!" + reset)
            for remaining in range(break_minutes * 60, 0, -1):
                sys.stdout.write(yellow + f"\rBreak Time left: {remaining // 60:02d}:{remaining % 60:02d}" + reset)
                sys.stdout.flush()
                time.sleep(1)
                
            print(green + "\n\n✨ Pomodoro session finished successfully!" + reset)
        except ValueError:
            print(red + "Please enter valid integers for timer durations." + reset)
    else:
        print(red, "Pomodoro not started.", reset)

#----------------------------------------MATH SOLVER-----------------------------------------
def math_solver():
    while True:
        print(cyan+"\n✨ MATH SOLVER ✨"+reset)
        print(yellow+"1. Square Root\n2. Power\n3. Factorial\n4. Trigonometry\n5. Log base 10\n6. Ceiling and Floor\n7. Exit"+reset)
        c = input("Enter choice: ").strip()
        try:
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
print(green,"Ceil =",math.ceil(n),reset)
print(green,"Floor =",math.floor(n),reset)
elif c=="7":
break
else:
print(red+"Invalid choice!"+reset)
except (ValueError, OverflowError):
print(red + f"Math Calculation Error: check inputs!" + reset)
#----------------------------------------GEOMETRY SOLVER-----------------------------------------
def geometry_solver():
while True:
print(magenta+"\n✨ GEOMETRY SOLVER ✨"+reset)
print(yellow+"1. Area of Square\n2. Area of Rectangle\n3. Area of Circle\n4. Volume of Cube\n5. Volume of Cylinder\n6. Exit"+reset)
choice=input("Choose: ").strip()
try:
if choice=="1":
side=float(input("Enter side: "))
print(green,"Area =",side2,reset)
elif choice=="2":
l=float(input("Length: "))
b=float(input("Breadth: "))
print(green,"Area =",lb,reset)
elif choice=="3":
r=float(input("Radius: "))
print(green,"Area =",math.pir2,reset)
elif choice=="4":
side=float(input("Side: "))
print(green,"Volume =",side3,reset)
elif choice=="5":
r=float(input("Radius: "))
h=float(input("Height: "))
print(green,"Volume =",math.pi*r2*h,reset)
elif choice=="6":
print(blue,"Exiting Geometry Solver...",reset)
break
else:
print(red+"Invalid choice!"+reset)
except ValueError:
print(red + "Invalid coordinate format or sizes." + reset)
#----------------------------------------PHYSICS SOLVER-----------------------------------------
def physics_solver():
while True:
print(magenta+"\n✨ PHYSICS SOLVER ✨"+reset)
print(yellow + "1. Speed d/t\n2. Distance st\n3. Acceleration (v-u)/t\n4. Force F=ma\n5. Work Done W=Fs\n6. Power P=W/t\n7. Kinetic Energy 0.5mv^2\n8. Weight W=mg\n9. Frequency f=1/T\n10. Exit" + reset)
choice=input("Choose: ").strip()
try:
if choice=="1":
d=float(input("Distance (m): "))
t=float(input("Time (s): "))
print(green,"Speed =",d/t,"m/s",reset)
elif choice=="2":
s=float(input("Speed: "))
t=float(input("Time: "))
print(green,"Distance =",st,"m",reset)
elif choice=="3":
u=float(input("Initial velocity: "))
v=float(input("Final velocity: "))
t=float(input("Time: "))
print(green,"Acceleration =", (v-u)/t,"m/s²",reset)
elif choice=="4":
m=float(input("Mass: "))
a=float(input("Acceleration: "))
print(green,"Force =", ma,"N",reset)
elif choice=="5":
f=float(input("Force: "))
d=float(input("Displacement: "))
print(green,"Work Done =", fd,"J",reset)
elif choice=="6":
w=float(input("Work Done: "))
t=float(input("Time: "))
print(green,"Power =", w/t,"W",reset)
elif choice=="7":
m=float(input("Mass: "))
v=float(input("Velocity: "))
print(green,"Kinetic Energy =", 0.5mv**2,"J",reset)
elif choice=="8":
m=float(input("Mass: "))
g=9.8
print(green,"Weight =", mg,"N",reset)
elif choice=="9":
T=float(input("Time Period: "))
print(green,"Frequency =",1/T,"Hz",reset)
elif choice=="10":
print(blue,"Exiting Physics Solver...",reset)
break
else:
print(red+"Invalid choice!"+reset)
except ZeroDivisionError:
print(red + "Time / Denominator parameter cannot be 0!" + reset)
except ValueError:
print(red + "Numeric configuration processing error." + reset)
#----------------------------------------CHEMISTRY SOLVER-----------------------------------------
def chemistry_solver():
while True:
print(cyan+"\n✨ CHEMISTRY SOLVER ✨"+reset)
print(yellow+"1. Number of Moles\n2. Mass\n3. Molarity\n4. Boyle's Law\n5. Charles's Law\n6. Percentage Composition\n7. Exit"+reset)
choice=input("Choose: ").strip()
try:
if choice=="1":
m=float(input("Mass: "))
M=float(input("Molar Mass: "))
print(green+"Moles =", m/M, reset)
elif choice=="2":
n=float(input("Moles: "))
M=float(input("Molar Mass: "))
print(green+"Mass =", nM, "g", reset)
elif choice=="3":
n=float(input("Moles: "))
V=float(input("Volume: "))
print(green+"Molarity =", n/V, "M", reset)
elif choice=="4":
P1=float(input("P1: "))
V1=float(input("V1: "))
P2=float(input("P2: "))
print(green+"V2 =", (P1V1)/P2, reset)
elif choice=="5":
V1=float(input("V1: "))
T1=float(input("T1: "))
T2=float(input("T2: "))
print(green+"V2 =", (V1*T2)/T1, reset)
elif choice=="6":
part=float(input("Mass of element: "))
whole=float(input("Molar mass of compound: "))
print(green+"Percentage =", (part/whole)*100, "%", reset)
elif choice=="7":
print(blue+"Exiting Chemistry Solver...",reset)
break
else:
print(red+"Invalid choice!"+reset)
except ZeroDivisionError:
print(red + "Calculations failed due to a division by zero error!" + reset)
except ValueError:
print(red + "Invalid input format parameters." + reset)
#----------------------------------------PHYSICS LIBRARY-----------------------------------------
def physics_library():
physics_dict = {
"acceleration": "Rate of change of velocity",
"amplitude": "Maximum displacement of a wave",
"angle": "Measure of rotation between two lines",
"atom": "Smallest unit of a chemical element",
"charge": "Property causing electromagnetic interaction",
"current": "Flow of electric charge",
"density": "Mass per unit volume",
"energy": "Ability to do work",
"force": "Push or pull causing acceleration",
"frequency": "Number of oscillations per second"
}
while True:
word = input(cyan + "\n🔍 Enter a physics word (or 'quit' to exit): " + reset).strip().lower()
if word == "quit":
print("👋 Exiting Physics Library!")
break
print(f"📚 {word}: {physics_dict.get(word, 'Word not found')}")
#----------------------------------------PYTHON LIBRARY-----------------------------------------
def python_library():
python_functions = {
"abs()": "Returns the absolute value of a number",
"all()": "Checks if all elements in an iterable are true",
"any()": "Checks if any element in an iterable is true",
"append()": "Adds an element to the end of a list",
"bin()": "Converts an integer to a binary string",
"bool()": "Converts a value to a boolean",
"dict()": "Creates a dictionary",
"enumerate()": "Returns an enumerate object",
"input()": "Gets user input",
"int()": "Converts a value to an integer",
"len()": "Returns the length of an object",
"list()": "Creates a list",
"print()": "Outputs text or values",
"range()": "Generates a sequence of numbers",
"sorted()": "Returns a sorted list",
"str()": "Converts a value to a string",
"sum()": "Returns the sum of an iterable",
"zip()": "Returns an iterator of tuples"
}
while True:
func = input(cyan+"🔍 Enter a Python function (e.g. len()) (or 'quit' to exit): "+reset).strip()
if func.lower() == "quit":
print("👋 Exiting Python Library!")
break
print(f"📚 {func}: {python_functions.get(func, 'Function not found (include brackets if stored that way)')}")
#----------------------------------------MAIN MENU-----------------------------------------
def mainmenu():
intro()
while True:
print(cyan + "\n" + "="*35 + " SERIFFY MENU " + "="*35 + reset)
print(yellow + "1. To-Do List            2. Percentage Calculator  3. Fortune Cookie" + reset)
print(yellow + "4. Unit Converter        5. Calculator             6. Pomodoro Timer" + reset)
print(yellow + "7. Math Homework Solver  8. Geometry Solver        9. Physics Solver" + reset)
print(yellow + "10. Chemistry Solver     11. Physics Library       12. Python Library" + reset)
print(yellow + "13. Countdown Timer      14. Exit" + reset)
choice = input("Enter your choice: ").strip()
if choice=="1": to_do_list()
elif choice=="2": percentage_calculator()
elif choice=="3": fortune_cookie()
elif choice=="4": converter()
elif choice=="5": calculator()
elif choice=="6": pomodoro()
elif choice=="7": math_solver()
elif choice=="8": geometry_solver()
elif choice=="9": physics_solver()
elif choice=="10": chemistry_solver()
elif choice=="11": physics_library()
elif choice=="12": python_library()
elif choice=="13": stopwatch()
elif choice=="14":
print(red+"Exiting SERIFFY...Study Hard!"+reset)
break
else:
print(red+"Invalid choice! Enter 1-14."+reset)
#----------------------------------------RUN PROGRAM-----------------------------------------
if name == "main":
mainmenu()


