<template>
    <v-form ref="form" v-model="valid">
        <v-text-field
            outline
            v-model="name"
            :rules="nameRules"
            label="Name"
            required
            clearable
        ></v-text-field>
        <v-text-field
            outline
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
            clearable
        ></v-text-field>
        <v-textarea
            outline
            label="Enter your Query here"
            v-model="query"
            :rules="queryRules"
            required
            :counter="200"
            clearable
        ></v-textarea>
        <v-btn :disabled="!valid" @click="submit">Submit</v-btn>
        <v-btn @click="reset">Reset</v-btn>
    </v-form>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            nameRules: [
                v => !!v || 'Name is required'
            ],
            email: '',
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+/.test(v) || 'E-mail must be valid'
            ],
            query: '',
            queryRules: [
                v => !!v || 'E-mail is required',
                v => (v && v.length <= 200) || 'Name must be less than 200 characters'
            ],
            valid: true
        }
    },
    methods: {
        submit() {
            if(this.$refs.form.validate()) {
                console.log('Submitting your query...')
            }
        },
        reset() {
            this.$refs.form.reset()
        }
    }
}
</script>

<style>

</style>
