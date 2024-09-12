<template>
  <div>
    <h1>Bienvenue sur la page d'accueil</h1>

    <!-- Intégration de la liste des taches -->
    <task-list></task-list>
  </div>
</template>

<script>
// Appel du composant TaskList
import TaskList from './task/TaskList.vue'

export default {
  components: {
    TaskList
  }
}
</script>
