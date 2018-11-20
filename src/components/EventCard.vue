<template>
    <v-card @mouseover="hover = true" @mouseout="hover = false" :to="`/event/${event.id}`">
        <v-card-text>
            <v-container fill-height>
                <v-layout align-center justify-center row fill-height v-if="!hover">
                    <v-flex sm12>
                        <div>
                            <h3>{{ event.name }}</h3>
                            <p>{{ event.venue }}</p>
                            <p>{{ event.date }}</p>
                            <p>{{ event.time }}</p>
                        </div>
                    </v-flex>
                </v-layout>

                <v-layout align-center justify-center row fill-height v-else>
                    <v-flex sm12>
                        <div>
                            <p>Summary: {{ event.desc }}</p>
                            <div>
                                <ul>
                                    <li v-for="(speaker, index) in event.speakers" :key="index">
                                        <img :src="speaker.imageUrl" :alt="`${speaker.name}\' photo`">
                                        {{ speaker.name }}
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-card-text>
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
