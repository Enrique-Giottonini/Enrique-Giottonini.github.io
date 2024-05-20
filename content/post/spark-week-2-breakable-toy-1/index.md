---
title: Encora Spark Week 3. Breakable Toy - To Do App [1/2]
date: 2024-05-19
math: true
---

# Takeaways from the week
- Hashing
- GenAI - Public Opinion and Education
- Project Planning for this week Assignment
- React revisited

Before receiving my assignment, I continued to explore topics in Skiena's "Algorithm Design". One blocker that had previously held me back from reading the book was the mental exhaustion that came with feeling like I needed to read the book from cover to cover. This time, I approached the book as a reference guide and went straight into a data structure that was important for my previous assignment: *hashing*.

# Hashing
Hash tables are a very practical way to maintain dictionaries, offering a nice constant time (or amortized constant time) for inserting, deleting, and searching items. They can be used to represent sets and maps (or dictionaries) with fast lookup. The `hash` is actually a function maps keys to integers, which represent the index of an array. 

We could in theory create unique identifiers for each key, but the corresponding array will grow too large. To avoid memory issues in practice, we limit the size of the array to m slots/buckets/bins using a modulo operation. The goal is to distribute the n key mappings uniformly so that each slot has approximately n/m items.

When two or more distincts keys are mapped to the same integer its called a collision.
I learned about two ways to deal with them: chaining and open addressing. **(1) Chaining** involves using an array of size m that points to the head of a linked list. Each time an element is added, it's put in the head of the hash(key) linked list. Searching an element involves searching the linked list of that key, which ideally should be amortized O(1) or n/m as m approaches n. **(2) Open addressing**, on the other hand, keeps the hash table as an array of elements. If there are collisions, we traverse the array to find an empty slot.

Chaining is more simple since its a combination of an array and growing linked list, but requires more memory overhead. In the other hand, open addressing makes the deletion of an element harder, as it might break a chain of insertions for keys that collides.

# Stanford AI Index Report 2024
In a team meeting, we discussed the direction of investments in the industry. The main theme was the growing interest in Data, Cloud, and GenAI. Those who aren't prepared for these technologies will soon be left behind. I read an interesting report from [Stanford's AI Lab](https://aiindex.stanford.edu/report/), which provides an overview of AI trends. I focused on the sections about public opinion and education.

I learned that although the number of computer science graduates is increasing, the number of those pursuing master's and Ph.D. degrees is not growing. Most students leave academia, and industry is leading the innovation in AI, thanks to their resources. Interestingly, less developed countries are more optimistic about AI and use tools like ChatGPT more frequently. People are starting to fear the impact of AI on their jobs, and companies are competing to stay ahead.

# Breakable Toy - To Do App

I was assigned to develop a mini-project, a to-do list app to help manage daily tasks. I will be using JavaScript and ReactJS for the frontend and Java Spring Boot for the backend. The project involves implementing a to-do app to manage tasks with a data table view with filtering, sorting, searching, and pagination.

I received the functional requirements, and the technical requirements in: UI, Model, API, Database, and version control.

The project is not complex per se, but I plan to take my time, digging more than necessary into the tools.

I planned my work by reviewing and clarifying requirements, breaking down requirements into tasks, estimating task durations, and implementing the frontend and backend. If the project was bigger I would also design a high-level architecture, and create user-stories. I was thinking about using [Atlassian](https://www.atlassian.com/) to track my progress since I heard is the way to go for most, but I plan to check it later.
I learned about the concept of "spikes" in kanban boards and created a kanban board in a blank page to track my progress.

This is how my kanban board ended up like:
![Kanban Board](/static/uploads/week3-kanban.png)

# React revisited

I revisited React and learned that components are just JavaScript functions that return markup, usually JSX. It's recommended to use an opinionated framework sitting on top of React, but I will be doing it vanilla. I needed to set up a custom build process with a bundler (that pipes all files into a single one) like [Vite](https://vitejs.dev/) or [Parcel](https://parceljs.org/). I will go with Vite since it seems easier to use and it's more [trendy](https://npmtrends.com/parcel-vs-vite) and has 20k more stars in GitHub.

After reading the documentation I feel like I already knew the basics of React such as component composition and `useState`. But I'm lacking in more complex features of react like `useMem`, or `useCallback`.

I created a modal component using React and learned about the useRef hook, which is used as a pointer/reference to a value that could change in the background but doesn't require a re-render. I also learned about `useEffect` hooks, which can be used to keep values in sync and run again if dependencies change.

## Example using vanilla JS and React
To create a modal, I can use the HTML5 dialog components, which are suitable for creating modals that prevent user interaction with the page, such as alerts, notifications, forms, and non-modal elements like cookie preferences and preferences panels.

```html
<button id="new-task"> Add Task </button>
<dialog id="add-task" class="modal">
  <h1> Create a new task </h1>
  <button id="close-task"> Close </button>
</dialog>
```

```js
const createNewTask = document.getElementById("add-task");
const newTaskButton = document.getElementById("new-task");
const closeTask = document.getElementById("close-task");

newTaskButton.addEventListener("click", () => {
  createNewTask.showModal();
})

closeTask.addEventListener("click", () => {
  createNewTask.close();
})
```

In React, you I created a modal component using the following code:

```javascript
import { useRef } from "react";

interface ModalProps {
    children: React.ReactNode
}

export default function Modal(props: ModalProps) {
    const modalRef = useRef< HTMLDialogElement | null >(null);
    return (
        <dialog ref={modalRef} className="modal">
            {props.children}
        </dialog>
    )
}
```

I learned that the `useRef` hook is used as a pointer/reference to a value that could change in the background but doesn't require a re-render. In this case is used to point to a DOM element, so other functions/effects inside the component have access to the dialog element.

We need to add more features to the Modal component...

```js
interface ModalProps {
	isOpen: boolean
	hasCloseBtn?: boolean
	onClose?: () => void
    children: React.ReactNode
}
```
And to handle them, we can use `useEffect` hook. I used to think that this hook was only as a run-once function, but I learned from the documentation that the dependencies parameter of the function is used to being kept in sync if they change, and if they do, the `useEffect` is run again. The reason it was run-once function is that I used an empty arrays of dependencies.

We use three hooks for our Modal template, dealing specifically with opening and closing a modal:

```js
export default function Modal(props: ModalProps) {
    ...
    const [isModalOpen, setModalOpen] = useState(props.isOpen);
    
    useEffect(() => {
        setModalOpen(props.isOpen);
    }, [props.isOpen]);
    
    useEffect(() => {
        const modalElement = modalRef.current;
        if (modalElement) {
            if (isModalOpen) modalElement.showModal();
            else             modalElement.close();
        }
    }, [isModalOpen]);
    ...
```
And two handlers:

```js
export default function Modal(props: ModalProps) {
	...
    function handleCloseModal() {
        if (props.onClose) props.onClose();
        setModalOpen(false);
    }

    function handleKeyDown(event: React.KeyboardEvent<HTMLDialogElement>) {
        if (event.key === "Escape") {
            handleCloseModal();
        }
    }
	...
```

And we can now use it in another component:

```js
export function NewTaskModal() {
  const [addingNew, setAddingNew] = useState(false);

  function handleOpenNewTask() {
    setAddingNew(true);
  }
  function handleCloseNewTask() {
    setAddingNew(false);
  }

  return (
    <>
        <button onClick={handleOpenNewTask}>+ New task </button>
        <Modal isOpen={addingNew} 
               hasCloseBtn={true} 
               onClose={handleCloseNewTask}>
                <p>Hello</p>
               </Modal>
    </>
```
The results looks good to me, so now I can close this Spike.
![New Task Modal](/static/uploads/w3-newtask.png)

This week was a great learning experience, and I'm excited to continue working on my project.