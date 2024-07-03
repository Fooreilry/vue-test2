<template>
  <v-app>
    <v-container>
      <h1>Опишите ваши любимые спортивные увлечения</h1>
      <v-btn color="primary" class="mt-4" @click="openDialog">Добавить</v-btn>
      <activities-table :activities="activities" @delete-activity="deleteActivity"/>
      <activitie-create-modal v-model="dialog" @add-activity="addActivity" @close-dialog="closeDialog"/>
    </v-container>
  </v-app>
</template>

<script>
import ActivitieCreateModal from './components/ActivitieCreateModal.vue'
import ActivitiesTable from './components/ActivitiesTable.vue'
export default {

  components: { ActivitiesTable, ActivitieCreateModal },

  data() {
    return {
      activities: [],
      dialog: false,
    }
  },

  methods: {
    openDialog() {
      this.dialog = true
    },

    resetNewActivity() {
      this.newActivity = {
        type: '',
        years: null,
        comment: '',
        bikeType: ''
      }
    },

    deleteActivity(activityId) {
      this.activities = this.activities.filter(({ id }) => id !== activityId)
    },

    addActivity(activityData) {
      this.activities.push({
        id: this.activities.length + 1,
        ...activityData
      })

      this.closeDialog()
    },

    closeDialog() {
      this.dialog = false
    },
  },

}
</script>