<template>
	<div>
		<v-img :aspect-ratio="16/9" max-height="80vh" src="https://images.unsplash.com/photo-1532178324009-6b6adeca1741?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=6f3285ad06f46abda5e0ff6d02594470&auto=format&fit=crop&w=1148&q=80">
			<v-layout align-center justify-center row fill-height class="lightbox white--text">
				<v-flex sm12>
					<div class="website-name">
						<h1>Delhi School of</h1>
						<h1>Artificial Intelligence</h1>
						<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam bibendum, tellus dapibus eleifend fringilla, velit magna semper lorem, vitae fermentum risus ante et tortor. Interdum et malesuada fames ac ante ipsum primis in faucibus.</p>
					</div>
				</v-flex>
			</v-layout>
		</v-img>
		<v-container>
			<v-layout align-center justify-center row fill-height>
				<v-flex sm12>
					<div class="section-heading">
						<h2>Upcoming Events</h2>
					</div>
				</v-flex>
			</v-layout>
			<v-layout align-center justify-center row fill-height mt-3>
				<v-flex xs12 sm6 md4 v-for="(event, index) in upcomingEvents" :key="index">
                    <event-card :event="event"></event-card>
                </v-flex>
			</v-layout>
		</v-container>
		<v-divider></v-divider>
		<v-container>
			<v-layout align-center justify-center row fill-height>
				<v-flex sm12>
					<div class="section-heading">
						<h2>Contact Us</h2>
					</div>
				</v-flex>
			</v-layout>
			<v-layout align-center justify-center row fill-height mt-3>
				<v-flex sm6>
					<ContactForm></ContactForm>
				</v-flex>
			</v-layout>
		</v-container>
	</div>
</template>

<script>
import db from '@/firebase/firebaseInit.js'
import EventCard from '@/components/EventCard.vue'
import ContactForm from '@/components/ContactForm.vue'
export default {
  name: 'home',
  data() {
	return {
	upcomingEvents: []
	}
  },
  created() {
	db.collection('events').where('date', '>=', new Date().toLocaleDateString()).get().then(querySnapshot => {
		querySnapshot.forEach(doc => {
			let tempEvent = doc.data()
			tempEvent.id = doc.id
			this.upcomingEvents.push(tempEvent)
		})
		console.log(this.upcomingEvents)
	})
  },
  components: {
	EventCard,
	ContactForm
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Raleway:500|Roboto+Slab');
	.website-name {
		max-width: 900px;
		margin: auto;
	}
	.website-name h1 {
		font-size: 5rem;
		text-align: center;
		font-family: 'Raleway', sans-serif;
		line-height: 100%;
	}
	.website-name p {
		/* padding: 20px 300px; */
		margin-top: 15px;
		text-align: center;
		color: rgb(216, 216, 216);
		font-family: 'Roboto Slab', serif;
	}
	.lightbox {
		background-color: rgba(0, 0, 0, 0.7);
	}
	.section-heading {
		font-size: 2rem;
		text-align: center;
		font-family: 'Raleway', sans-serif;
	}
</style>

