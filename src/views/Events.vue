<template>
    <v-container fluid>
        <v-layout align-center justify-center row fill-height>
            <v-flex sm12>
                <div class="section-heading">
                    <h1>Events</h1>
                </div>
            </v-flex>
        </v-layout>
        <v-container>
            <v-layout align-center justify-center row fill-height mt-5>
                <v-flex sm12>
                    <div class="section-sub-heading">
                        <h1>Upcoming Events</h1>
                    </div>
                    <v-divider></v-divider>
                </v-flex>
            </v-layout>
            <v-layout align-center justify-center row fill-height px-3>
                <v-flex xs12 sm6 md4 v-for="(event, index) in upcomingEvents" :key="index">
                    <event-card :event="event"></event-card>
                </v-flex>
            </v-layout>
        </v-container>
        <v-container>
            <v-layout align-center justify-center row fill-height mt-5>
                <v-flex sm12>
                    <div class="section-sub-heading">
                        <h1>Past Events</h1>
                    </div>
                    <v-divider></v-divider>
                </v-flex>
            </v-layout>
            <v-layout align-center justify-center row fill-height px-3>
                <v-flex xs12 sm6 md4 v-for="(event, index) in pastEvents" :key="index">
                    <event-card :event="event"></event-card>
                </v-flex>
            </v-layout>
        </v-container>
    </v-container>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
export default {
    name: 'events',
    data() {
        return {
            pastEvents: [],
            upcomingEvents: []
        }
    },
    components: {
        UpcomingEvents,
        EventCard
    },
    created() {
        // To-DO pull all the past events from Firebase and add them to this.pastEvents array.
        // TO-DO pull all the upcoming events from Firebase and add them to this.upcomingEvents array.
    }
}
</script>

<style>
    .section-sub-heading {
        font-family: 'Roboto', serif;
    }
</style>
