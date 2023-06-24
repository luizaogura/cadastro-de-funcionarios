<template>
  <div>
    <h1>Gerenciamento de Funcionários</h1>

    <h2>Cadastro de Funcionário</h2>
    <div class="container">
    <form @submit.prevent="addEmployee">
      <div class="row">
      <label for="name">Nome:</label>
      <input type="text" id="name" v-model="newEmployee.name" required>
      </div>

      <label for="lastName">Sobrenome:</label>
      <input type="text" id="lastName" v-model="newEmployee.lastName" required>

      <label for="age">Idade:</label>
      <input type="number" id="age" v-model="newEmployee.age" required>
      <div>
        <label for="position">Cargo:</label>
        <input type="text" id="position" v-model="newEmployee.position" required>
      </div>
      <label for="startDate">Data de Início:</label>
      <input type="date" id="startDate" v-model="newEmployee.startDate" required>
      <div>
      <label for="active">Ativo:</label>
      <input type="checkbox" id="active" v-model="newEmployee.active">
      </div>
      <div>
      <button type="submit">Cadastrar</button>
      </div>
    </form>
  </div>

    <h2>Listagem de Funcionários</h2>
    <ul>
      <li v-for="employee in employees" :key="employee.id" @click="editEmployee(employee)">
        {{ employee.name }} {{ employee.lastName }} - {{ employee.position }}
        <button @click.stop="deleteEmployee(employee)">Excluir</button>
      </li>
    </ul>

    <h2 v-if="selectedEmployee">Atualização de Dados de Funcionário</h2>
    <form v-if="selectedEmployee" @submit.prevent="updateEmployee">
      <label for="edit-name">Nome:</label>
      <input type="text" id="edit-name" v-model="selectedEmployee.name" required>

      <label for="edit-lastName">Sobrenome:</label>
      <input type="text" id="edit-lastName" v-model="selectedEmployee.lastName" required>

      <label for="edit-age">Idade:</label>
      <input type="number" id="edit-age" v-model="selectedEmployee.age" required>

      <label for="edit-position">Cargo:</label>
      <input type="text" id="edit-position" v-model="selectedEmployee.position" required>

      <label for="edit-startDate">Data de Início:</label>
      <input type="date" id="edit-startDate" v-model="selectedEmployee.startDate" required>

      <label for="edit-active">Ativo:</label>
      <input type="checkbox" id="edit-active" v-model="selectedEmployee.active">

      <button type="submit">Salvar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      employees: [],
      newEmployee: {
        id: '',
        name: '',
        lastName: '',
        age: '',
        position: '',
        startDate: '',
        active: false,
        creator: ''
      },
      selectedEmployee: null
    }
  },
  methods: {
    addEmployee() {
      this.employees.push({ ...this.newEmployee });
      this.newEmployee = {
        id: '',
        name: '',
        lastName: '',
        age: '',
        position: '',
        startDate: '',
        active: false,
        creator: ''
      };
    },
    editEmployee(employee) {
      this.selectedEmployee = { ...employee };
    },
    updateEmployee() {
      this.selectedEmployee = null;
    },
    deleteEmployee(employee) {
      const confirmDelete = confirm('Tem certeza que deseja excluir o funcionário?');
      if (confirmDelete) {
        this.employees = this.employees.filter(emp => emp.id !== employee.id);
      }
    }
  }
}
</script>

<style>

  body {
    background: rgb(210,210,210);
  }
  * {
  box-sizing: border-box;
}

input[type=text], select, textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: vertical;
}

input[type=number] {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: vertical;
}

label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

input[type=submit] {
  background-color: #04AA6D;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  float: right;
}

input[type=submit]:hover {
  background-color: #45a049;
}

.container {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

.col-25 {
  float: left;
  width: 25%;
  margin-top: 6px;
}

.col-75 {
  float: left;
  width: 75%;
  margin-top: 6px;
}

@media screen and (max-width: 600px) {
  .col-25, .col-75, input[type=submit] {
    width: 100%;
    margin-top: 0;
  }
}

</style>
