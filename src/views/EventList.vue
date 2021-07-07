<template>
	<h1>Events for Good</h1>
	<div class="events">
		<EventCard v-for="event in events" :key="event.id" :event="event" />
	</div>
</template>

<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import EventService from "@/services/EventService.js";

export default {
	name: "EventList",
	components: {
		EventCard,
	},
	data() {
		return {
			events: null,
		};
	},
	created() {
		EventService.getEvents()
			.then((res) => {
				console.log("Events:", res.data);
				this.events = res.data;
			})
			.catch((err) => {
				console.log("Errors:", err);
			});
	},
};
</script>

<style scoped>
.events {
	display: flex;
	flex-direction: column;
	align-items: center;
}
</style>
