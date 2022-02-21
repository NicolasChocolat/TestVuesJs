<template>
  <form @submit.prevent>
    <div>
      <label for="name">Name :</label>
      <input v-model="name" type="text" name="name" />
    </div>
    <div>
      <label for="date">Date :</label>
      <input v-model="date" type="date" name="date" />
    </div>
    <div>
      <label for="note">Note :</label>
      <input v-model="note" name="note" type="text" />
    </div>
    <button @click="addUser()">Ajouter</button>
  </form>

  <table class="tableau">
    <tr>
      <td>Nom</td>
      <td>Date</td>
      <td>Note</td>
    </tr>
    <tr v-for="user in users" :key="user.id">
      <td>{{ user.name }}</td>
      <td>{{ user.date }}</td>
      <td>{{ user.note }}</td>
    </tr>
  </table>
  <div v-if="isData">
    <canvas id="myChart" width="400" height="400"></canvas>
  </div>
</template>

<script>
import { uuid } from "vue-uuid";

export default {
  data() {
    return {
      isData: false,
      users: [
        {
          id: "",
          name: "",
          date: "",
          note: "",
        },
      ],
    };
  },
  methods: {
    addUser() {
      this.users.push({
        id: uuid.v1(),
        name: this.name,
        date: this.date,
        note: this.note,
      });
      this.isData = true;
    },
  },
  mounted() {
    if (localStorage) {
      localStorage.setItem("name-user", this.name);
      localStorage.setItem("date-user", this.date);
      localStorage.setItem("note-user", this.note);
    }
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 1px solid #1b1b1b;
  margin: 2rem;
  border-radius: 60px;
}
input {
  margin: 2rem;
}
button {
  margin: 1rem;
}
input {
  border-radius: 4px;
}

table {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border: 1px solid #1b1b1b;
  margin: 2rem;
  text-align: center;
}

td {
  padding: 0 3rem;
}
</style>
