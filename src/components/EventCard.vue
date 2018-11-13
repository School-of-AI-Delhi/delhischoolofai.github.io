<template>
    <v-card @mouseover="hover = !hover" :to="`/event/${event.id}`">
        <v-img :src="event.imageLinks[0]">
            <v-container fill-height>
                <v-layout align-center justify-center row fill-height v-show="hover">
                    <v-flex sm12>
                        <div>
                            <h3>{{ event.title }}</h3>
                            <p>{{ event.venue }}</p>
                            <p>{{ event.date }}</p>
                        </div>
                    </v-flex>
                </v-layout>

                <v-layout align-center justify-center row fill-height v-show="!hover">
                    <v-flex sm12>
                        <div>
                            <p>Summary: {{ event.description }}</p>
                            <div>
                                <ul>
                                    <li v-for="(speaker, index) in event.speakers" :key="index">
                                        <img :src="speaker.imageLink" :alt="`${speaker.name}\' photo`">
                                        {{ speaker.name }}
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-img>
        <v-card-actions v-if="isUpcoming">
            <v-btn color="primary">Register</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    props: ['event'],
    data() {
        return {
            hover: false
        }
    },
    computed: {
        isUpcoming: function() {
            if(this.event.date > new Date()) {
                return true
            } else {
                return false
            }
        }
    }
}
</script>

<style>

</style>
