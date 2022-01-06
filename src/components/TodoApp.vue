<template>
  <div class="container grid-md my-3">
    <h2>Liste des choses à faires</h2>

  <div class="input-group">
    <input v-model="task" @keyup.enter="submitTask" class="form-input input-lg" type="text" placeholder="Entrer une nouvelle tâche">
    <button @click="submitTask" class="btn btn-primary input-group-btn btn-lg">Ajouter</button>
  </div>

<table class="table table-striped table-hover my-3">
  <thead>
    <tr>
      <th>Tâches</th>
      <th>État</th>
      <th class="fix-w">#</th>
      <th class="fix-w">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(tasks, index) in tasks" :key="index">
      <td>{{tasks.name}}</td>
      <td>{{tasks.status}}</td>
      <td class="fix-w" @click="editTask"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path></svg></td>
      <td class="fix-w" @click="deleteTask"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-delete"><path d="M21 4H8l-7 8 7 8h13a2 2 0 0 0 2-2V6a2 2 0 0 0-2-2z"></path><line x1="18" y1="9" x2="12" y2="15"></line><line x1="12" y1="9" x2="18" y2="15"></line></svg></td>
    </tr>
  </tbody>
</table>

  </div>
</template>

<script>
export default {
  
  data() {
    return {
      task: '',
      tasks: [
        {
          name: 'Streal bananas from the store.',
          status: 'à faire'
        },
        {
          name: 'Une autre tache',
          status: 'en cours'
        }
      ]
      
    }
  },

  methods: {
    submitTask() {
      if(this.task.lenght === 0) return;

      this.tasks.push({
        name: this.task,
        status: 'à faire'
      })
      this.task = '';
    }
  }
  
};
</script>

<style scoped>
.fix-w {
  text-align: center;
  width: 4rem;
}
</style>