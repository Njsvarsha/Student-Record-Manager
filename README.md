import re

FILE_NAME = "students.txt"


# Validate email using Regex
def validate_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email)


# Add student
def add_student():
    try:
        roll_no = input("Enter Roll Number: ")

        if not roll_no.isdigit():
            raise ValueError("Roll Number must contain only numbers.")

        name = input("Enter Student Name: ")

        if not name.strip():
            raise ValueError("Name cannot be empty.")

        email = input("Enter Email: ")

        if not validate_email(email):
            raise ValueError("Invalid email format.")

        # Save student data to file
        with open(FILE_NAME, "a") as file:
            file.write(roll_no + "," + name + "," + email + "\n")

        print("Student added successfully!")

    except ValueError as e:
        print("Invalid Input:", e)


# Read student data
def read_students():
    try:
        with open(FILE_NAME, "r") as file:
            data = file.readlines()

            if not data:
                print("No student records found.")
                return

            print("\n--- Student Records ---")

            for line in data:
                roll_no, name, email = line.strip().split(",")
                print("Roll Number:", roll_no)
                print("Name:", name)
                print("Email:", email)
                print("-----------------------")

    except FileNotFoundError:
        print("No student file found. Please add a student first.")

    except Exception as e:
        print("Error:", e)


# Main menu
def main():
    while True:
        print("\n===== Student Record Manager =====")
        print("1. Add Student")
        print("2. Read Student Data")
        print("3. Exit")

        try:
            choice = int(input("Enter your choice: "))

            if choice == 1:
                add_student()

            elif choice == 2:
                read_students()

            elif choice == 3:
                print("Program exited.")
                break

            else:
                print("Please enter a number between 1 and 3.")

        except ValueError:
            print("Invalid input! Please enter a number.")


main()
