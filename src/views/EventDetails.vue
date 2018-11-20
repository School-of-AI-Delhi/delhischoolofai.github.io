<template>
    <v-card>
        <v-card-title>
            <div class="event-title">
                {{ event.name }}
            </div>
        </v-card-title>
        <v-card-text>
            <div>
                <div class="description">
                    <span>Description:</span>
                    <p>{{ event.desc }}</p>
                </div>
                <div class="venue">
                    <p><span>Venue:</span> {{ event.venue }}</p>
                </div>
                <div class="date">
                    <p><span>Date:</span> {{ event.date }}</p>
                </div>
                <div class="time">
                    <p><span>Time:</span> {{ event.time }}</p>
                </div>
                <div class="prereqs">
                    <span>Prerequisites:</span>
                    <v-layout align-center justify-center row fill-height>
                        <v-flex xs12 sm6 md4 lg3 v-for="(prereq, index) in event.prereqs" :key="index">
                            {{ prereq }}
                        </v-flex>
                    </v-layout>
                </div>
                <div class="speakers">
                    <v-layout align-center 
                            justify-center 
                            row 
                            fill-height
                            class="speaker" 
                            v-for="(speaker, index) in event.speakers" 
                            :key="index">
                        <v-flex sm3>
                            <div class="speaker-photo">
                                <img :src="speaker.imageUrl" :alt="`${speaker.name}\' photo`">
                            </div>
                        </v-flex>
                        <v-flex sm4>
                            <div class="speaker-name">
                                <h3>{{ speaker.name }}</h3>
                            </div>
                            <div class="speaker-summary">
                                <p>{{ speaker.details }}</p>
                            </div>
                        </v-flex>
                        <v-flex sm5>
                            <div class="speaker-social-links">
                                <div class="social-image">
                                    <a :href="speaker.facebookUrl" v-if="speaker.facebookUrl">
                                        <!-- <img src="@/assets/facebook.png" alt="facebook icon"> -->
                                    </a>
                                    <a :href="speaker.twitterUrl" v-if="speaker.twitterUrl">
                                        <!-- <img src="@/assets/twitter.png" alt="twitter icon"> -->
                                    </a>
                                    <a :href="speaker.githubUrl" v-if="speaker.githubUrl">
                                        <!-- <img src="@/assets/github.png" alt="github icon"> -->
                                    </a>
                                    <a :href="speaker.linkedInUrl" v-if="speaker.linkedInUrl">
                                        <!-- <img src="@/assets/linkedIn.png" alt="linkedIn icon"> -->
                                    </a>
                                </div>
                            </div>
                        </v-flex>
                    </v-layout>
                </div>
            </div>
            <div>
                <h3>Register</h3>
                <v-divider></v-divider>
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
                    <v-btn :disabled="!valid" @click="register" color="primary">Register</v-btn>
                    <v-btn @click="reset">Reset</v-btn>
                </v-form>
            </div>
        </v-card-text>
    </v-card>
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
            valid: true
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
    }
}
</script>

<style>

</style>
