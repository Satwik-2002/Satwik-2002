class Task:
    def __init__(self, description):
        self.description = description
        self.completed = False

    def mark_complete(self):
        self.completed = True

    def __str__(self):
        status = "✔️" if self.completed else "❌"
        return f"{status} {self.description}"
        import pickle
import os

class ToDoList:
    def __init__(self):
        self.tasks = []

    def add_task(self, description):
        self.tasks.append(Task(description))

    def view_tasks(self):
        if not self.tasks:
            print("No tasks available.")
        for idx, task in enumerate(self.tasks, start=1):
            print(f"{idx}. {task}")

    def update_task(self, task_index, new_description):
        if 0 <= task_index < len(self.tasks):
            self.tasks[task_index].description = new_description
        else:
            print("Invalid task number.")

    def delete_task(self, task_index):
        if 0 <= task_index < len(self.tasks):
            del self.tasks[task_index]
        else:
            print("Invalid task number.")

    def mark_task_complete(self, task_index):
        if 0 <= task_index < len(self.tasks):
            self.tasks[task_index].mark_complete()
        else:
            print("Invalid task number.")

    def save_tasks(self, filename="tasks.pkl"):
        with open(filename, 'wb') as file:
            pickle.dump(self.tasks, file)

    def load_tasks(self, filename="tasks.pkl"):
        if os.path.exists(filename):
            with open(filename, 'rb') as file:
                self.tasks = pickle.load(file)

def display_menu():
    print("\nTo-Do List Menu")
    print("1. Add Task")
    print("2. View Tasks")
    print("3. Update Task")
    print("4. Delete Task")
    print("5. Mark Task as Complete")
    print("6. Save Tasks")
    print("7. Load Tasks")
    print("8. Exit")

def main():
    todo_list = ToDoList()
    while True:
        display_menu()
        choice = input("Choose an option: ")
        if choice == '1':
            description = input("Enter task description: ")
            todo_list.add_task(description)
        elif choice == '2':
            todo_list.view_tasks()
        elif choice == '3':
            task_index = int(input("Enter task number to update: ")) - 1
            new_description = input("Enter new task description: ")
            todo_list.update_task(task_index, new_description)
        elif choice == '4':
            task_index = int(input("Enter task number to delete: ")) - 1
            todo_list.delete_task(task_index)
        elif choice == '5':
            task_index = int(input("Enter task number to mark as complete: ")) - 1
            todo_list.mark_task_complete(task_index)
        elif choice == '6':
            todo_list.save_tasks()
            print("Tasks saved successfully.")
        elif choice == '7':
            todo_list.load_tasks()
            print("Tasks loaded successfully.")
        elif choice == '8':
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

