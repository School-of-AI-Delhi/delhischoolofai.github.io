<template>
    <v-card>
        <v-card-media>
            <v-carousel>
                <v-carousel-item v-for="(imageLink, index) in event.imageLinks" :key="index" :src="imageLink"></v-carousel-item>
            </v-carousel>
        </v-card-media>
        <v-card-title>
            <div class="event-title">
                {{ event.title }}
            </div>
        </v-card-title>
        <v-card-text>
            <div>
                <div class="description">
                    <span>Description</span>
                    <p>{{ event.description }}</p>
                </div>
                <div class="venue">
                    <p><span>Venue:</span> {{ event.venue }}</p>
                </div>
                <div class="timing">
                    <p><span>Timing:</span> {{ event.date }}</p>
                </div>
                <div class="requirements">
                    <span>Requirements:</span>
                    <v-layout align-center justify-center row fill-height>
                        <v-flex xs12 sm6 md4 lg3 v-for="(requirement, index) in event.requirements" :key="index">
                            {{ requirement }}
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
                                <img :src="speaker.imageLink" :alt="`${speaker.name}\' photo`">
                            </div>
                        </v-flex>
                        <v-flex sm4>
                            <div class="speaker-name">
                                <h3>{{ speaker.name }}</h3>
                            </div>
                            <div class="speaker-summary">
                                <p>{{ speaker.summary }}</p>
                            </div>
                        </v-flex>
                        <v-flex sm5>
                            <div class="speaker-social-links">
                                <div class="social-image">
                                    <a :href="speaker.socialLink">
                                        <img :src="`@/assets/${speaker.socialName}.png`" :alt="`${speaker.socialName} Icon`">
                                    </a>
                                </div>
                            </div>
                        </v-flex>
                    </v-layout>
                </div>
            </div>
            <v-divider></v-divider>
            <div>
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
                    <v-btn :disabled="!valid" @click="submit">Submit</v-btn>
                    <v-btn @click="reset">Reset</v-btn>
                </v-form>
            </div>
        </v-card-text>
    </v-card>
</template>

<script>
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
