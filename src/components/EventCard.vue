<template>
    <v-card @mouseover="hover = true" @mouseout="hover = false" :to="`/event/${event.id}`">
        <v-card-text>
            <v-container fill-height>
                <v-layout align-center justify-center row fill-height v-if="!hover">
                    <v-flex sm12>
                        <div class="event-details">
                            <h2>{{ event.name }}</h2>
                            <v-divider></v-divider>
                            <p><span class="heading">Venue:</span> {{ event.venue }}</p>
                            <p><span class="heading">Date:</span> {{ event.date }}</p>
                            <p><span class="heading">Time:</span> {{ event.time }}</p>
                        </div>
                    </v-flex>
                </v-layout>

                <v-layout align-center justify-center row fill-height v-else>
                    <v-flex sm12>
                        <div>
                            <p><span class="heading">Summary:</span> {{ event.desc }}</p>
                            <div class="speakers">
                                <ul>
                                    <li v-for="(speaker, index) in event.speakers" :key="index">
                                        <v-layout>
                                            <v-flex xs4>
                                                <img :src="speaker.imageUrl" :alt="`${speaker.name}\' photo`">
                                            </v-flex>
                                            <v-flex xs8>
                                                <span class="speaker-name"> {{speaker.name }}</span>
                                                <br>
                                                <span> {{ speaker.details }} </span>
                                            </v-flex>
                                        </v-layout>
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
    .heading {
        font-weight: 600;
        font-size: 1.2rem;
        color: #484242;
    }
    .event-details p{
        margin-top: 10px;
    }
    .speakers ul {
        list-style: none;
        padding: 0px;
    }
    .speakers ul li{
        margin-bottom: 10px;
    }
    .speakers ul li img {
        max-width: 70px;
    }
    .speakers ul li .speaker-name {
        font-weight: 500;
    }
</style>
