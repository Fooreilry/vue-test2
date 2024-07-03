<template>
    <v-table class="elevation-1 mt-4 mb-4">
        <thead>
            <tr class="text-left bg-primary text-white text-h6 weight-bold">
                <th>№</th>
                <th>Название</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <template v-if="activities.length">
                <tr class="p-4 text-subtitle-1 weight-bold" v-for="activity in activities" :key="activity.id">
                    <td>{{ activity.id }}</td>
                    <td>{{ activity.type }}</td>
                    <td>
                        <v-btn color="error" @click="deleteActivity(activity.id)">Удалить</v-btn>
                    </td>
                </tr>
            </template>
            <tr class="text-center p-4" v-else>
                <td colspan="3">Нет активностей</td>
            </tr>
        </tbody>
    </v-table>
</template>

<script>
export default {

    props: {
        activities: {
            type: Array,
            required: true
        }
    },

    emits: ['delete-activity'],

    methods: {
        deleteActivity(activityId) {
            this.$emit('delete-activity', activityId)
        }
    }

}
</script>

<style>

</style>