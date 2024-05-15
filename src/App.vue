<template>
  <div id="app">
    <div class="background">
      <div class="todo-app">
        <h1>
          List Tontonan Film
        </h1>
        <div class="nama">
          <h3>
            Serlina Siregar
          </h3>
          <h3>
            223510016
          </h3>
        </div>
        <div class="inputcontener">
          <input v-model="newTodo" placeholder="Tambahkan List Film" @keyup.enter="addTodo" /> <!-- # menambahkan list pada todo -->
          <button @click="addTodo" class="action-button">Tambahkan</button>
        </div>
        <ul>
          <li v-for="(todo, index) in todos" :key="index"> 
            <div v-if="!todo.editing"> <!-- # mengedit inputan todo sebelumnya -->
              <span :class="{ done: todo.done }" @click="toggleDone(index)"> 
                {{ todo.text }} 
              </span>
              <button @click="editTodo(index)" class="action-button">Edit</button>
              <button @click="deleteTodo(index)" class="action-button">Delete</button>
            </div>
            <div v-else>
              <input v-model="todo.text" @keyup.enter="saveEdit(index)" /> 
              <button @click="saveEdit(index)" class="action-button">Save</button>
              <button @click="cancelEdit(index)" class="action-button">Cancel</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '', 
      todos: [],   
    };
  },

  // menambahkan list inputan pada todo
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({ text: this.newTodo });
        this.newTodo = ''; 
      }
    },
    // mengetdit inputan todo yang telah di input sebelumnya 
    editTodo(index) {
      const newText = prompt('Edit list film', this.todos[index].text);
      if (newText !== null) {
        this.todos[index].text = newText;
      }
    },
    // Menghapus list todo yang telah di input sebelumnya
    deleteTodo(index) {
      if (confirm('Apakah anda ingin menghapus list film tersebut?')) {
        this.todos.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
* {
  color: white; /* Setel warna font menjadi putih untuk semua elemen */
}

.background {
  background-image: url('https://img.freepik.com/free-vector/creative-geometric-design-space_53876-89781.jpg?t=st=1715694358~exp=1715697958~hmac=0678cc2bb4fc00532be0dfe9abb45d68261ce4e8b432b930e97ba2928a7fa834&w=740');
  background-size: cover;
  background-position: center;
  background-color: rgba(255, 255, 255, 10); 
}

.nama {
  margin-top: 5px;
  text-align: left;
}

.inputcontener {
  display: flex;
  align-items: center;
  margin-top: 30px;
  text-align: center;
}

.todo-app {
  max-width: 500px;
  margin: 0 auto;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: rgba(128, 128, 128, 0.8); /* Menambahkan warna abu-abu pada kotak todo */
}

input {
  margin-right: 1rem;
  padding: 0.5rem;
  font-size: 1rem;
  color: black; /* Kecuali input untuk memudahkan melihat teks yang diketik */
}

button {
  margin-left: 0.5rem;
  padding: 0.5rem;
  font-size: 1rem;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 0;
}

.done {
  text-decoration: line-through;
  color: #aaa;
}

.action-button {
  color: black; /* Membuat warna font tombol action menjadi hitam */
}
</style>