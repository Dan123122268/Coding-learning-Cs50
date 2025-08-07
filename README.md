# Coding-learning-Cs50
A list of projects and assingments based on and inspired by lectures from CS50
# CS50 Python Mini Projects

This repository contains a collection of beginner-friendly Python projects inspired by the [CS50 Introduction to Programming with Python](https://cs50.harvard.edu/python/2022/) course.
Each project uses concepts learned in the course and can be expanded into more complex applications as you progress.

---

## 📁 Project List

### 1. Flashcard Quiz App
- **Topics:** File I/O, Lists, CSV, Random, Loops
- **Description:** Quiz the user on questions loaded from a `.csv` file.
```python
import csv, random

with open("flashcards.csv") as f:
    reader = list(csv.reader(f))
    random.shuffle(reader)
    score = 0
    for question, answer in reader:
        user = input(f"{question}: ")
        if user.lower() == answer.lower():
            print("Correct!")
            score += 1
        else:
            print(f"Wrong. Correct answer: {answer}")
    print(f"Final score: {score}/{len(reader)}")
```

---

### 2. Contact Manager
- **Topics:** File I/O, CSV, Dictionaries
- **Description:** Add and search contacts in a CSV file.
```python
import csv

def add_contact():
    name = input("Name: ")
    email = input("Email: ")
    with open("contacts.csv", "a", newline='') as file:
        writer = csv.writer(file)
        writer.writerow([name, email])

def search_contact():
    query = input("Search name: ").lower()
    with open("contacts.csv", newline='') as file:
        reader = csv.reader(file)
        for row in reader:
            if query in row[0].lower():
                print("Found:", row)

while True:
    choice = input("1) Add 2) Search 3) Exit: ")
    if choice == "1":
        add_contact()
    elif choice == "2":
        search_contact()
    else:
        break
```

---

### 3. Rock, Paper, Scissors
- **Topics:** Random, Conditionals
- **Description:** A CLI game vs. the computer.
```python
import random

choices = ["rock", "paper", "scissors"]
while True:
    user = input("Your move (rock/paper/scissors/quit): ").lower()
    if user == "quit":
        break
    if user not in choices:
        print("Invalid choice.")
        continue
    comp = random.choice(choices)
    print(f"Computer chose {comp}")
    if user == comp:
        print("It's a tie!")
    elif (user == "rock" and comp == "scissors") or \
         (user == "paper" and comp == "rock") or \
         (user == "scissors" and comp == "paper"):
        print("You win!")
    else:
        print("You lose!")
```

---

### 4. To-Do List (CLI)
- **Topics:** Lists, Loops
- **Description:** Simple terminal-based to-do manager.
```python
tasks = []

def show_tasks():
    for i, task in enumerate(tasks, 1):
        print(f"{i}. {task}")

while True:
    action = input("Add / Show / Remove / Exit: ").lower()
    if action == "add":
        task = input("Enter task: ")
        tasks.append(task)
    elif action == "show":
        show_tasks()
    elif action == "remove":
        show_tasks()
        i = int(input("Which task to remove (number)? "))
        tasks.pop(i - 1)
    elif action == "exit":
        break
    else:
        print("Unknown command.")
```

---

### 5. Dice Roller
- **Topics:** Random, Functions
- **Description:** Simulates rolling a dice.
```python
import random

def roll_dice():
    print("You rolled:", random.randint(1, 6))

while True:
    cmd = input("Roll the dice? (y/n): ").lower()
    if cmd == "y":
        roll_dice()
    else:
        break
```

---

### 6. Gradebook Manager
- **Topics:** Dictionaries, Conditionals
- **Description:** Stores student names and grades, and classifies them.
```python
grades = {}

while True:
    name = input("Student name (or 'done'): ")
    if name == "done":
        break
    score = int(input("Score: "))
    grades[name] = score

for name, score in grades.items():
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    else:
        grade = "C or below"
    print(f"{name}: {score} ({grade})")
```

---

### 7. Personal Budget Tracker (Final Project)
- **Topics:** File I/O, Functions, Lists, Dictionaries, JSON, Error Handling, Modular Design
- **Description:** A CLI app to track expenses, view summaries, and save/load data to a JSON file. 

```python
import json, os

DATA_FILE = "budget_data.json"

def load_data():
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, "r") as file:
            return json.load(file)
    return []

def save_data(data):
    with open(DATA_FILE, "w") as file:
        json.dump(data, file, indent=4)

def add_expense(data):
    category = input("Category (e.g. Food, Rent, Transport): ")
    try:
        amount = float(input("Amount: $"))
    except ValueError:
        print("Invalid amount.")
        return
    data.append({"category": category, "amount": amount})
    print("Expense added.")

def view_summary(data):
    print("\nExpense Summary:")
    summary = {}
    for entry in data:
        cat = entry["category"]
        amt = entry["amount"]
        summary[cat] = summary.get(cat, 0) + amt
    for cat, amt in summary.items():
        print(f"{cat}: ${amt:.2f}")
    print(f"Total: ${sum(summary.values()):.2f}\n")

def main():
    data = load_data()
    while True:
        print("\n1) Add Expense 2) View Summary 3) Exit")
        choice = input("Choose an option: ")
        if choice == "1":
            add_expense(data)
            save_data(data)
        elif choice == "2":
            view_summary(data)
        elif choice == "3":
            break
        else:
            print("Invalid option.")

if __name__ == "__main__":
    main()
```

---
