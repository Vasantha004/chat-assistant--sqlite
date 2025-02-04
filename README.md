# chat-assistant--sqlite
# Chat Assistant with SQLite

## Overview
A simple Flask-based chat assistant that queries an SQLite database using natural language.

## Features
- Supports queries like:
  - "Show me all employees in [department]."
  - "Who is the manager of [department]?"
  - "List all employees hired after [date]."

## Setup
### 1. Clone the Repo
```sh
git clone https://github.com/your-username/chat-assistant-sqlite.git
cd chat-assistant-sqlite

import os

def init_db():
    if not os.path.exists("employees.db"):  # Check if DB exists
        conn = sqlite3.connect("employees.db")
        cursor = conn.cursor()
        
        # Create Employees table
        cursor.execute("""
        CREATE TABLE IF NOT EXISTS Employees (
            ID INTEGER PRIMARY KEY,
            Name TEXT,
            Department TEXT,
            Salary INTEGER,
            Hire_Date TEXT
        )""")
        
        # Create Departments table
        cursor.execute("""
        CREATE TABLE IF NOT EXISTS Departments (
            ID INTEGER PRIMARY KEY,
            Name TEXT,
            Manager TEXT
        )""")
        
        # Insert sample data
        cursor.executemany("INSERT OR IGNORE INTO Employees VALUES (?, ?, ?, ?, ?)", [
            (1, "Alice", "Sales", 50000, "2021-01-15"),
            (2, "Bob", "Engineering", 70000, "2020-06-10"),
            (3, "Charlie", "Marketing", 60000, "2022-03-20")
        ])
        
        cursor.executemany("INSERT OR IGNORE INTO Departments VALUES (?, ?, ?)", [
            (1, "Sales", "Alice"),
            (2, "Engineering", "Bob"),
            (3, "Marketing", "Charlie")
        ])
        
        conn.commit()
        conn.close()
        print("Database initialized!")  # Debug message
