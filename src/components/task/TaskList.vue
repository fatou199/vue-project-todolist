<template>
  <div class="box">
    <!-- Ajouter des taches -->
    <!-- Champ de saisie pour ajouter une nouvelle tâche -->
    <input v-model="newTask" placeholder="Ajouter une tâche" />

    <!-- Bouton pour ajouter une nouvelle tâche -->
    <button @click="addTask">Ajouter</button>

    <!-- Condition pour afficher le nombre de tache -->
    <p v-if="tasks.length === 0">Aucune tâche à afficher</p>
    <p v-else>Nombre de tâches : {{ tasks.length }}</p>

    <!-- Affichage de la liste des tâches -->
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

        <!-- Si la tache n'est pas en mode edition -->
        <div class="list" v-else>
          <div class="task-container">
            <!-- Checkbox pour marquer la tache comme terminée -->
            <input type="checkbox" v-model="task.done" @change="storageTasks" />
            <!-- Texte de la tâche, barré si elle est terminée -->
            <span v-bind:class="{ completed: task.done }">{{ task.name }}</span>
          </div>

          <!-- Bouton pour modifier et supprimer la tache -->
          <div class="button-container">
            <button @click="editTask(index)">Modifier</button>
            <button @click="deleteTask(index)">Supprimer</button>
          </div>
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
      // Récupère les tâches sauvegardées dans le Local Storage
      // Si aucune tâche n'est sauvegardée, le tableau est vide par défaut
      // JSON.parse pour convertir les données en tableau
      tasks: JSON.parse(localStorage.getItem('tasks')) || []
    }
  },

  methods: {
    // Ajouter une tâche
    addTask() {
      // verifie si le champ contient une valeur ou non
      if (this.newTask) {
        // Ajout d'une nouvelle tâche
        this.tasks.push({
          // Génèration d'un id unique pour la tâche en fonction de la longueur du tableau
          id: this.tasks.length + 1,
          // Stocke le texte de la nouvelle tâche
          name: this.newTask,
          // Par defaut isEdit n'est pas modifiable
          isEdit: false,
          // Par defaut la tache n'est pas terminée
          done: false
        })
        this.newTask = '' // Reinitialise le champ de saisie
        this.storageTasks() // Sauvegarde dans le Local Storage
      }
    },

    // Modifier la tâche
    editTask(index) {
      this.tasks[index].isEdit = true
    },

    // Mettre à jour la tache
    updateTask(index) {
      this.tasks[index].isEdit = false
      this.storageTasks()
    },

    // Annuler la modification de la tâche
    cancelTask(index) {
      this.tasks[index].isEdit = false
      this.storageTasks()
    },

    // Supprimer une tâche
    deleteTask(index) {
      this.tasks.splice(index, 1)
    },

    // Sauvegarde les tâches dans le Local Storage
    storageTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    }
  }
}
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
