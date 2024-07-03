<template>
    <v-dialog v-model="this.dialog" max-width="500px">
        <v-card>
            <v-card-title>Добавить активность</v-card-title>
            <v-card-text>
                <v-select v-model="newActivity.type" :items="activityTypes" label="Выберите активность"></v-select>
                <v-text-field v-model.number="newActivity.years" label="Сколько лет увлекаетесь"
                    type="number"></v-text-field>
                <v-textarea v-model="newActivity.comment" label="Комментарий"></v-textarea>
                <v-select v-if="newActivity.type === 'велосипеды'" v-model="newActivity.bikeType" :items="bikeTypes"
                    label="Тип велосипеда"></v-select>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDialog">Отменить</v-btn>
                <v-btn color="blue darken-1" text @click="addActivity">Добавить</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
export default {

    props: {
        dialog: {
            type: Boolean,
            required: true
        }
    },

    emits: ['close-dialog', 'add-activity'],

    data() {
        return {
            newActivity: {
                type: '',
                years: null,
                comment: '',
                bikeType: ''
            },
            activityTypes: [
                'горные лыжи', 'виндсерфинг', 'кайтсерфинг', 'сноуборды',
                'плавание', 'яхтинг', 'боулинг', 'велосипеды'
            ],
            bikeTypes: ['шоссейные', 'горные', 'bmx']
        }
    },

    methods: {
        addActivity() {
            this.$emit('add-activity', this.newActivity)
            this.resetNewActivity()
        },
        
        closeDialog() {
            this.$emit('close-dialog')
            this.resetNewActivity()
        },
        
        resetNewActivity() {
            this.newActivity = {
                type: '',
                years: null,
                comment: '',
                bikeType: ''
            }
        }
    }
}
</script>

<style></style>