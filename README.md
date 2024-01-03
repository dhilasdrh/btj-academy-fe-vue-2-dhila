# Task 2 JavaScript Framework (Vue)

This code is a refactored version of previous To Do App that utilized two-way binding. In this task, the code has been organized into several components such as SummaryCard, SummarySection, AddTaskSection, MessageDisplay, TaskCard, TaskList, and TaskListSection. The application allows users to add, delete, and mark tasks as done.

## Code Summary

#### App.vue:

-   This component is the main entry point for the application.
-   It uses a `BaseLayout` component as its main layout.
-   Utilizes various child components such as `HeaderSection`, `SummarySection`, `AddTaskSection`, `TaskListSection`, and `FooterSection`.
-   Makes use of named slots (`v-slot`) to structure the layout and insert content dynamically into specific sections of the layout.
-   Utilizes computed properties to filter tasks based on completion status and priority.
-   Implements methods for adding new tasks, handling task deletion, marking tasks as done, and updating local storage.
-   The component is mounted by retrieving tasks from local storage.

#### BaseLayout:

-   Acts as a base layout for the application, providing a structured container for different sections.
-   Uses `slot` to dynamically insert content into the header, summary, addTask, taskList, and footer sections.

#### SummaryCard:

-   Represents a card displaying a summary of tasks based on priority.
-   Dynamically applies styles based on the priority of tasks.

#### SummarySection:

-   Displays a summary of pending and priority-based tasks using `SummaryCard` components.
-   Utilizes props to receive task counts.
-   Demonstrates the use of a watch and mounted lifecycle hooks.

#### AddTaskSection:

-   Provides a form for adding new tasks.
-   Emits events to the parent component when a new task is added or an error occurs.
-   Uses two-way data binding (`v-model`) for form inputs.
-   Utilizes a custom `Message` component for displaying success or error messages.

#### MessageDisplay:

-   A reusable component for displaying messages with dynamic styles.
-   Accepts props for visibility, title, message, border color, background color, and text color.

#### TaskCard:

-   Represents a card displaying individual tasks.
-   Utilizes props to receive task information.
-   Emits events to the parent component when a task is deleted or marked as done.
-   Dynamically applies styles based on task priority.

#### TaskList:

-   Displays a list of tasks using `TaskCard` components.
-   Uses props to receive the title, tasks, and an empty message to display when there are no tasks.
-   Emits events to the parent component when a task is deleted or marked as done.
-   Demonstrates the use of lifecycle hooks (`created`, `mounted`, `beforeDestroy`) and a watcher for tasks.

#### TaskListSection:

-   Contains two instances of the `TaskList` component, one for displaying todo tasks and another for completed tasks.
-   Uses props to pass todo and completed tasks, as well as empty messages.
-   Emits events to the parent component when a task is deleted or marked as done.

### Concepts Used


1.  **Components:**
    
The application is organized into multiple components (`App`, `BaseLayout`, `SummaryCard`, `SummarySection`, `AddTaskSection`, `MessageDisplay`, `TaskCard`, `TaskList`, and `TaskListSection`) for better maintainability and reusability.

2.  **Lifecycle Hooks:**
    
The `mounted` lifecycle hook is used in the `App` component to check for stored tasks in the local storage and initialize the tasks.

3.  **Slots:**
    
The `BaseLayout` component uses slots to define the structure of the layout, allowing child components (`HeaderSection`, `SummarySection`, `AddTaskSection`, `TaskListSection`, and `FooterSection`) to inject their content into specific areas.

4.  **Computed Properties:**
    
Computed properties are used in the `App` component to dynamically calculate the total number of tasks, pending tasks, low/medium/high priority tasks, etc.

5.  **Event Handling:**
    
Events are emitted and handled to communicate between parent and child components. For example, the `addNewTask`, `deleteTask`, and `markAsDone` methods emit events in child components, and the corresponding methods handle these events in the parent (`App`) component.

6.  **Dynamic Styling:**
    
Dynamic styling is achieved through conditional classes in components like `SummaryCard` and `MessageDisplay`. The color of the cards and messages depends on the priority or the type of message.

7.  **Form Handling:**
    
The `AddTaskSection` component includes a form for adding new tasks. It uses two-way data binding (`v-model`) to update the `newTask` data property based on user input.

8.  **LocalStorage Usage:**
    
The application uses `localStorage` to store tasks persistently. The `updateLocalStorage` and `getStoredTasks` methods in the `App` component handle the saving and retrieval of tasks from local storage.

9.  **Watchers:**
    
The `watch` option is used in the `TaskList` component to monitor changes in the `tasks` array.
