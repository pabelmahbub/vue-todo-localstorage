
### vue-todo-localstorage
### Live site: https://vue-todo-localstorage.netlify.app/
### develop app with the follwoing commands:
```
a. npm init vue@latest
b. naming app[my-app]
c. cd my-app
d. npm i
e. npm run dev
```
```
import { ref, onMounted, computed, watch } from 'vue'
```
Defining varibale inside ref:
```
const todos = ref([])
const name = ref('')
const input_content = ref('')
const input_category = ref(null)
```
Todo data serializing:
```
const todos_asc = computed(() => todos.value.sort((a,b) =>{
	return a.createdAt - b.createdAt
}))
```
Local storage data save and retrieve:
```
watch(name, (newVal) => {
	localStorage.setItem('name', newVal)
})

watch(todos, (newVal) => {
	localStorage.setItem('todos', JSON.stringify(newVal))
}, {deep: true})
```
Pushing data in todo array:
```
const addTodo = () => {
	if (input_content.value.trim() === '' || input_category.value === null) {
		return
	}
	todos.value.push({
		content: input_content.value,
		category: input_category.value,
		done: false,
		editable: false,
		createdAt: new Date().getTime()
	})
}
```
Remove todo data from array:
```
const removeTodo = (todo) => {
	todos.value = todos.value.filter((t) => t !== todo)
}
```
Local storage data retrieve:
```
onMounted(() => {
	name.value = localStorage.getItem('name') || ''
	todos.value = JSON.parse(localStorage.getItem('todos')) || []
})
```

