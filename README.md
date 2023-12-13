# ✅ todo-app-vue

A simple "to-do list for the day" application with extremely basic functionality, built with Vite + Vue 3, TypeScript, and Bootstrap.

A user is able to:
- Add a unique task item to the list
- Check off task items from the list
- Remove all task items from the list
- View persisted tasks in list after page refresh

## 🎯 Goals

- Implement and understand Vue concepts (e.g. form input binding, data reactivity)
- Design components based on functionality and reusability (e.g. `ListItem.vue` vs `ListCard.vue`)
- Introduce and implement concepts of local storage
- Learn how to install and use Bootstrap

## 📸 Project Screenshots

![TODO-Built-with-Vue_New-Tasks](https://github.com/priyanka-kishore/todo-app-vue/assets/33528287/6d1056c3-fa4e-4f72-b72d-dfcb3bbafc65)
![TODO-Built-with-Vue_Some-Checked](https://github.com/priyanka-kishore/todo-app-vue/assets/33528287/e27e07f9-ec94-41f2-8a8f-73f6376c6f12)
![TODO-Built-with-Vue_All-Checked](https://github.com/priyanka-kishore/todo-app-vue/assets/33528287/72709ebb-1ec9-44ac-9709-860ad07225c1)
![TODO-Built-with-Vue_Duplicate-Task](https://github.com/priyanka-kishore/todo-app-vue/assets/33528287/7dc3101c-97c1-40a0-b232-35b2f8b94ed5)
![TODO-Built-with-Vue_No-Tasks](https://github.com/priyanka-kishore/todo-app-vue/assets/33528287/288811bb-753d-4236-a577-b3afe67d61d4)

## 🛠️ Local Project Setup

To run this project locally, clone/download this repo and install `npm` on your machine.

#### 🔨 Install dependencies listed in `package.json`:
```sh
npm install
```

#### 🔨 Compile and Hot-Reload for Development:

```sh
npm run dev
```

#### 🔨 Type-Check, Compile and Minify for Production:

```sh
npm run build
```

#### 🔨 Lint with [ESLint](https://eslint.org/):

```sh
npm run lint
```

## 🌱 Reflection

- What was the context for this project?
- What did you set out to build?
- Why was this project challenging and therefore a really good learning experience?
- What were some unexpected obstacles?
- What tools did you use to implement this project?

This was a week long project built after my full-time work hours at my front end developer job. The goal for creating and completing this project was to apply the frontend skills I learned on the job (after previously working as a Java backend developer) to a fairly easy side project.

I set out to build a relatively simply to-do list application that has the most basic functionalities of adding a task to a list, checking off tasks on that list, and removing all tasks at once from the list.

The beginning of this project was challenging when figuring out which build tools to use to stand up a basic scaffolding of the project. I ended up using Vite since that is what the frontend teams use at my job. Another challenge was deciding how I wanted to break down the reusable components to prevent redundancy. I had to design how and which data was sent between components as well as creating types to enforce type-safety.

Some unexpected obstacles were figuring out how to pass data between child and parent components so that the to-do list item data was kept synchronized. At first, I used `props` and `emit`, but quickly realized using two-way binding with `v-model` would be a better way. Also, another obstacle was ensuring reactivity when the list would change with more or checked off items. I had to make sure that the original list was not replaced, but rather `spliced` from or `pushed` to in order to maintain reactivity.

I decided to use the Vue JS framework as this was my first frontend JS framework I ever used thanks to work. I plan to recreate the project in React JS as well to learn the basics. I used TypeScript instead of JavaScript to enforce typing, and Bootstrap to learn how to install and use a third-party styling and component library, instead of sticking with plain CSS/SCSS like I use at work. I also used Vite to bundle everything and build the project for development and production.
