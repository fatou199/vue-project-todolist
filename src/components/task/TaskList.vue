<template>
  <div>
    <!-- Champ de saisie pour ajouter une nouvelle tâche -->
    <input v-model="newTask" placeholder="Ajouter une tâche" />

    <!-- Bouton pour ajouter une nouvelle tâche -->
    <button @click="addTask">Ajouter</button>

    <!-- Liste des tâches -->
    <ul>
      <!-- Pour chaque tache m'afficher un element de liste -->
      <!-- v-bind:key donne une clé unique à chaque tâche -->
      <li v-for="(task, index) in tasks" v-bind:key="task.id">
        <!-- Si la tache est en mode edition -->
        <div class="list" v-if="task.isEdit">
          <!-- Champ de saisie lié à la propriété "name" de l'objet "task" -->
          <input v-model="task.name" />
          <button @click="updateTask(index)">Enregistrer</button>
          <button @click="cancelTask(index)">Annuler</button>
        </div>

        <div class="list" v-else>
          <!-- Checkbox pour marquer la tache comme faite -->
          <input type="checkbox" v-model="task.done" />
          <!-- Affichage du nom de la tache -->
          <span class="">{{ task.name }}</span>

          <!-- Bouton pour modifier et supprimer la tache -->
          <button @click="editTask(index)">Modifier</button>
          <button @click="deleteTask(index)">Supprimer</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Variable pour stocker le texte de la nouvelle tâche
      newTask: '',
      // Tableau vide pour stocker les tâches
      tasks: []
    }
  },

  methods: {
    addTask() {
      // Ajout d'une nouvelle tâche
      this.tasks.push({
        // Génèration d'un id unique pour la tâche en fonction de la longueur du tableau
        id: this.tasks.length + 1,
        // Stocke le texte de la nouvelle tâche
        name: this.newTask,
        // Par defaut isEdit n'est pas modifiable
        isEdit: false
      })
      // Reinitialise le champ de saisie
      this.newTask = ''
    },

    // Modifier la tâche
    editTask(index) {
      this.tasks[index].isEdit = true
    },

    // Mettre à jour la tache
    updateTask(index) {
      this.tasks[index].isEdit = false
    },

    cancelTask(index) {
      this.tasks[index].isEdit = false
    },

    // Supprimer une tâche
    deleteTask(index) {
      this.tasks.splice(index, 1)
    }
  }
}
</script>
