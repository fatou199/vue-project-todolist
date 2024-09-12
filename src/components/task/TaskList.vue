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
        <!-- Checkbox pour marquer la tache comme faite -->
        <input type="checkbox" v-model="task.done" />
        <!-- Affichage du nom de la tache -->
        <span class="">{{ task.name }}</span>
        <!-- Bouton pour modifier et supprimer la tache -->
        <button @click="updateTask(index)">Modifier</button>
        <button @click="deleteTask(index)">Supprimer</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
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
        name: this.newTask
      })
      // Reinitialise le champ de saisie
      this.newTask = ''
    }
  }
}
</script>
