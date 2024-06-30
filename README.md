# simple-task-list-la
class Task:
    def __init__(self, description, priority):
        self.description = description
        self.priority = priority

class TaskManager:
    def __init__(self):
        self.tasks = []

    def add_task(self, description, priority):
        task = Task(description, priority)
        self.tasks.append(task)

    def remove_task(self, description):
        for task in self.tasks:
            if task.description == description:
                self.tasks.remove(task)
                print(f"Task '{description}' removed.")
                return
        print(f"Task '{description}' not found.")

    def list_tasks(self):
        if not self.tasks:
            print("No tasks found.")
        else:
            print("Tasks:")
            for i, task in enumerate(self.tasks, start=1):
                print(f"{i}. Description: {task.description}, Priority: {task.priority}")

    def prioritize_tasks(self):
        self.tasks.sort(key=lambda x: x.priority, reverse=True)
        print("Tasks prioritized.")

    def recommend_task(self, keyword):
        recommended_task = None
        max_score = 0
        for task in self.tasks:
            score = self.calculate_similarity(task.description, keyword)
            if score > max_score:
                max_score = score
                recommended_task = task
        if recommended_task:
            print(f"Recommended Task: {recommended_task.description}")
        else:
            print("No recommended task found.")

    def calculate_similarity(self, description, keyword):
        # Example simple scoring function (you can use more sophisticated methods)
        score = 0
        for word in description.lower().split():
            if word == keyword.lower():
                score += 1
        return score

# Example usage
if __name__ == "__main__":
    task_manager = TaskManager()

    task_manager.add_task("Complete project report", 2)
    task_manager.add_task("Prepare presentation slides", 1)
    task_manager.add_task("Review meeting agenda", 3)

    task_manager.list_tasks()

    task_manager.remove_task("Prepare presentation slides")
    task_manager.list_tasks()

    task_manager.prioritize_tasks()
    task_manager.list_tasks()

    task_manager.recommend_task("report")
