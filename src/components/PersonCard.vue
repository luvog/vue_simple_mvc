<template>
  <div class="person-card">
    <b-card  bg-variant="dark" text-variant="white" :title="person.name">
      <p class="card-text">Eye's color: {{person.eye_color}}</p>
      <p class="card-text">Car's color: {{person.car_color}}</p>
      <p class="card-text">House's color: {{person.house_color}}</p>
    </b-card>
  </div>
</template>

<script>
export default {
  name: 'PersonCard',
  props: {
    person: Object
  }
}
</script>

<style scoped>
	.person-card {
		margin-bottom: 10px;
	}
</style>
