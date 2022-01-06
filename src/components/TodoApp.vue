<template>
	<div class="container grid-md my-3">
		<h2>Liste des choses à faires</h2>

		<div class="input-group">
			<input v-model="task" @keyup.enter="submitTask" class="form-input input-lg" type="text" placeholder="Entrer une nouvelle tâche" />
			<button @click="submitTask" class="btn btn-primary input-group-btn btn-lg">Ajouter</button>
		</div>

		<table class="table table-striped table-hover my-3">
			<thead>
				<tr>
					<th>Tâches</th>
					<th>État</th>
					<th class="table-action">#</th>
					<th class="table-action">#</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="(tasks, index) in tasks" :key="index">
					<td :class="{'finished' : tasks.status === 'Terminée'}">{{ tasks.name }}</td>
					<td class="table-status"><span @click="changeStatus(index)" :class="{'text-success' : tasks.status === availableStatues[2], 'text-warning' : tasks.status === availableStatues[1], 'text-error' : tasks.status === availableStatues[0]}">{{ tasks.status }}</span></td>
					<td class="table-action" @click="editTask(index)">
						<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-edit">
							<path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
							<path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
						</svg>
					</td>
					<td class="table-action" @click="deleteTask(index)">
						<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-delete">
							<path d="M21 4H8l-7 8 7 8h13a2 2 0 0 0 2-2V6a2 2 0 0 0-2-2z"></path>
							<line x1="18" y1="9" x2="12" y2="15"></line>
							<line x1="12" y1="9" x2="18" y2="15"></line>
						</svg>
					</td>
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
      editedTask: '',
      availableStatues: ['À faire', 'En cours', 'Terminée'],
      tasks: [
        {
          name: 'Streal bananas from the store.',
          status: 'À faire'
        },
        {
          name: 'Une autre tâche',
          status: 'En cours'
        }
      ]
    }
  },

  methods: {
    submitTask() {
      if(this.task.lenght === 0) return;

      if(this.editedTask === '') {
        this.tasks.push({
          name: this.task,
          status: this.availableStatues[0]
        })
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    editTask(index) {
      this.task = this.tasks[index].name
      this.editedTask = index;
    },

    changeStatus(index) {
      let nextIndex = this.availableStatues.indexOf(this.tasks[index].status);
      if( nextIndex++ > (this.availableStatues.lenght - 1)) nextIndex = 0;
      this.tasks[index].status = this.availableStatues[nextIndex];

    }
  }

};
</script>

<style>
.table-action {
	text-align: center;
	width: 4rem;
}
.table-action > svg {
	cursor: pointer;
}
.table-status {
  cursor: pointer;
  width: 6rem;
}
.finished {
  text-decoration: line-through;
}
</style>
