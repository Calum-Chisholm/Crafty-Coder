<template lang="html">
  <table>
    <tr>
      <th>Name:</th>
      <th>Email:</th>
      <th>Checked in</th>
      <th></th>
    </tr>
    <tr v-for="booking in bookings">
      <td>{{booking.name}}</td>
      <td>{{booking.email}}</td>
      <td><input  type="checkbox" name="checked_in" v-if="booking.checked_in" checked></td>
      <td><input  v-on:click="deleteBooking(booking._id)" type="submit" value="Delete"></td>
  </tr>
</table>
</template>

<script>
import { eventBus } from '@/main.js'
import HotelService from '@/services/HotelService.js'

export default {
  name: "guest-table",
  data(){
    return {
      bookings: []
    }
  },
  methods: {
    deleteBooking(id){
      HotelService.deleteBooking(id)
      let index = this.bookings.findIndex(booking => booking._id === id)
      this.bookings.splice(index, 1)
    }
  },
  mounted(){
    HotelService.getBookings()
    .then(bookings => this.bookings = bookings)

    eventBus.$on('booking-added', (booking) => {
      this.bookings.push(booking)
    })
  },
}
</script>

<style lang="css" scoped>
</style>
