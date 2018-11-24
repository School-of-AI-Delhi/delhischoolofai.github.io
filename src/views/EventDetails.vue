<template>
    <v-container>
        <v-card>
            <v-card-title>
                <div class="event-title">
                    <h1>{{ event.name }}</h1>
                </div>
            </v-card-title>
            <v-card-text>
                <div>
                    <div class="description">
                        <span class="heading">Description:</span>
                        <p>{{ event.desc }}</p>
                    </div>
                    <div class="venue">
                        <p><span class="heading">Venue:</span> {{ event.venue }}</p>
                    </div>
                    <div class="date">
                        <p><span class="heading">Date:</span> {{ event.date }}</p>
                    </div>
                    <div class="time">
                        <p><span class="heading">Time:</span> {{ event.time }}</p>
                    </div>
                    <div class="prereqs">
                        <h3 class="heading">Prerequisites:</h3>
                        <span class="prereq primary" v-for="(prereq, index) in event.prereqs" :key="index">{{ prereq }}</span>
                    </div>
                    
                    <span class="heading">Speakers:</span>
                    <v-layout align-center justify-center row fill-height class="speaker">
                        <v-flex xs12 
                            v-for="(speaker, index) in event.speakers" 
                            :key="index">
                            <v-layout>
                                <v-flex sm3>
                                    <div class="speaker-image">
                                        <img :src="speaker.imageUrl" :alt="`${speaker.name}\' photo`">
                                    </div>
                                </v-flex>
                                <v-flex sm9 class="speaker-details">
                                    <div class="speaker-name">
                                        <h3>{{ speaker.name }}</h3>
                                    </div>
                                    <div class="speaker-summary">
                                        <p>{{ speaker.details }}</p>
                                    </div>
                                    <div class="speaker-social-links">
                                        <div class="social-image">
                                            <a :href="speaker.facebookUrl" v-if="speaker.facebookUrl">
                                                <img src="@/assets/facebook.png" alt="facebook icon">
                                            </a>
                                            <a :href="speaker.twitterUrl" v-if="speaker.twitterUrl">
                                                <img src="@/assets/twitter.png" alt="twitter icon">
                                            </a>
                                            <a :href="speaker.githubUrl" v-if="speaker.githubUrl">
                                                <img src="@/assets/github.png" alt="github icon">
                                            </a>
                                            <a :href="speaker.linkedinUrl" v-if="speaker.linkedinUrl">
                                                <img src="@/assets/linkedin.png" alt="linkedIn icon">
                                            </a>
                                        </div>
                                    </div>
                                </v-flex>
                            </v-layout>
                        </v-flex>
                    </v-layout>    
                </div>
                <div v-if="totalRegistrations <= event.maxAttendees">
                    <span class="heading">Register Here:</span>
                    <v-form ref="form" v-model="valid" class="registration-form">
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
                        <v-btn :disabled="!valid" @click="register" color="primary">Register</v-btn>
                        <v-btn @click="reset">Reset</v-btn>
                    </v-form>
                </div>
                <div v-else class="registration-ended">
                    <p class="error">Registrations have been closed for this event!</p>
                </div>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<script>
import db from '@/firebase/firebaseInit.js'
export default {
    data() {
        return {
            event: {},
            name: '',
            nameRules: [
                v => !!v || 'Name is required'
            ],
            email: '',
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+/.test(v) || 'E-mail must be valid'
            ],
            valid: true,
            totalRegistrations: 0
        }
    },
    methods: {
        register() {
            if(this.$refs.form.validate()) {
                let user = {
                    name: this.name,
                    email: this.email,
                    date: new Date().toLocaleDateString(),
                    eventId: this.$route.params.eventId
                }
                db.collection('registeredUsers').add(user).then(docRef => {
                    alert('You have successfully registered for the event')
                    this.$router.push('/')
                })
            }
        },
        reset() {
            this.$refs.form.reset()
        }
    },
    created() {
        db.collection('events').doc(this.$route.params.eventId).get().then(doc => {
            if(doc.exists) {
                this.event = doc.data()
            }
        })
        db.collection('registeredUsers').where('eventId', '==', this.$route.params.eventId).get().then(querySnapshot => {
            this.totalRegistrations = querySnapshot.size
        })
    }
}
</script>

<style scoped>
    .event-title {
        margin: auto;
    }
    .heading {
        font-weight: 600;
        font-size: 1.2rem;
        color: #484242;
    }
    .prereq {
        font-weight: 500;
        background-color: #ff5252;
        color: white;
        padding: 10px;
        border-radius: 30px;
        margin-right: 10px;
    }
    .prereqs h3 {
        margin-bottom: 20px;
    }
    .prereqs {
        margin-bottom: 20px;
    }
    .speaker {
        margin: 20px;
    }
    .speaker-image img {
        max-height: 150px;
        max-width: 120px;
        border-radius: 2px;
    }
    .social-image a img{
        max-width: 30px;
    }
    .social-image a {
        margin-right: 10px;
    }
    .speaker-details {
        margin-left: 30px;
    }
    .registration-form {
        margin: 20px 0px;
    }
    .error {
        padding: 10px;
        color: white;
        border-radius: 20px;
        font-size: 1.3rem;
        font-weight: 500;
    }
    .registration-ended {
        margin-top: 40px;
        text-align: center;
    }
</style>
