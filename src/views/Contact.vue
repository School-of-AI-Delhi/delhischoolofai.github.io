<template>
    <v-container>
        <v-layout align-center justify-center row fill-height>
            <v-flex sm12>
                <div class="section-heading">
                    <h1>Contact us</h1>
                </div>
            </v-flex>
        </v-layout>
        <v-layout align-center justify-center row fill-height mt-3>
            <v-flex sm8>
                <contact-form></contact-form>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue'
export default {
    name: 'contact',
    components: {
        ContactForm
    }
}
</script>

<style scoped>

</style>
