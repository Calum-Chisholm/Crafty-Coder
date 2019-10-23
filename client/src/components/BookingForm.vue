<template lang="html">
  <form class="" v-on:submit.prevent="addBooking">
    <label for="name">Name:</label>
    <input type="text" id="name" v-model="name" required/>
    <label for="email">Email:</label>
    <input type="text" id="email" v-model="email" required/>
    <input type="submit" value="Save" id="save"/>
  </form>
</template>

<script>
import { eventBus } from '@/main.js'
import HotelService from '@/services/HotelService.js'
export default {
  name: 'booking-form',
  data(){
    return {
      name: '',
      email: null,
      checked_in: false
      }
    },
    methods: {
      addBooking(){
        const booking = {
          name: this.name,
          email: this.email,
          checked_in: this.checked_in
        }
        HotelService.postBooking(booking)
        .then(res => eventBus.$emit('booking-added', res))
      }
    }
  }
</script>
<style lang="css" scoped>

</style>
