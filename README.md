# Collection-manipulater
# Student Data Organizer - Collection Manipulator

def display_welcome():
    """Display welcome message and program overview"""
    print("=" * 50)
    print("Welcome to the Student Data Organizer!")
    print("=" * 50)
    print("This program helps you manage student records.")
    print("You can add, view, update, and delete student information.")
    print("Each student record includes: name, age, grade, and subjects.\n")


# Dictionary to store student records {ID: {details}}
students = {}

# Set to store unique subjects
all_subjects = set()


def add_student():
    """Add a new student record"""
    try:
        student_id = int(input("Enter Student ID (unique number): "))  # Type casting
        if student_id in students:
            print("⚠️ Student ID already exists! Please try again.\n")
            return

        name = input("Enter Student Name: ")
        age = int(input("Enter Age: "))
        grade = input("Enter Grade: ")

        # Tuple for immutable info (ID, DOB)
        dob = input("Enter Date of Birth (DD-MM-YYYY): ")
        immutable_info = (student_id, dob)

        # Subjects
        subjects = input("Enter subjects (comma-separated): ").split(",")
        subjects = [sub.strip().title() for sub in subjects]
        all_subjects.update(subjects)  # Add to set (ensures uniqueness)

        # Save record in dictionary
        students[student_id] = {
            "immutable": immutable_info,
            "name": name,
            "age": age,
            "grade": grade,
            "subjects": subjects
        }
        print(f"✅ Student {name} added successfully!\n")

    except ValueError:
        print("❌ Invalid input! Please enter numbers where required.\n")


def view_students():
    """View all student records"""
    if not students:
        print("No student records available.\n")
        return

    print("=" * 50)
    print("All Student Records".center(50))
    print("=" * 50)

    for sid, details in students.items():
        # f-string formatting
        print(f"ID: {sid}")
        print(f"Name: {details['name']}")
        print(f"Age: {details['age']}")
        print(f"Grade: {details['grade']}")
        print(f"Subjects: {', '.join(details['subjects'])}")
        print(f"Immutable Info (ID, DOB): {details['immutable']}")
        print("-" * 50)
    print()


def update_student():
    """Update student details"""
    try:
        student_id = int(input("Enter Student ID to update: "))
        if student_id not in students:
            print("❌ Student not found!\n")
            return

        print("What do you want to update?")
        print("1. Name")
        print("2. Age")
        print("3. Grade")
        print("4. Subjects")
        choice = input("Enter choice: ")

        if choice == "1":
            students[student_id]["name"] = input("Enter new name: ")
        elif choice == "2":
            students[student_id]["age"] = int(input("Enter new age: "))
        elif choice == "3":
            students[student_id]["grade"] = input("Enter new grade: ")
        elif choice == "4":
            subjects = input("Enter new subjects (comma-separated): ").split(",")
            subjects = [sub.strip().title() for sub in subjects]
            students[student_id]["subjects"] = subjects
            all_subjects.update(subjects)
        else:
            print("❌ Invalid choice!\n")
            return

        print("✅ Student details updated successfully!\n")

    except ValueError:
        print("❌ Invalid input! Please enter numbers where required.\n")


def delete_student():
    """Delete a student record"""
    try:
        student_id = int(input("Enter Student ID to delete: "))
        if student_id in students:
            del students[student_id]  # Using del keyword
            print("✅ Student record deleted successfully!\n")
        else:
            print("❌ Student not found!\n")
    except ValueError:
        print("❌ Invalid input! Please enter a valid ID.\n")


def view_subjects():
    """View all unique subjects"""
    print("=" * 50)
    print("Unique Subjects Offered".center(50))
    print("=" * 50)
    print(", ".join(sorted(all_subjects)) if all_subjects else "No subjects available.\n")
    print()


# Main menu
def main():
    display_welcome()

    while True:
        print("Menu:")
        print("1. Add Student")
        print("2. View Students")
        print("3. Update Student")
        print("4. Delete Student")
        print("5. View Unique Subjects")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            update_student()
        elif choice == "4":
            delete_student()
        elif choice == "5":
            view_subjects()
        elif choice == "6":
            print("Exiting program... Goodbye!")
            break
        else:
            print("❌ Invalid choice! Please try again.\n")


# Run the program
if __name__ == "__main__":
    main()
