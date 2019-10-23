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
      <td><i class="far fa-check-circle" v-if="booking.checked_in"></i><i class="far fa-times-circle" v-if="!booking.checked_in"></i></td>
      <td><input  v-on:click="deleteBooking(booking._id)" type="submit" value="Delete"></td>
      <td><input  v-on:click="checkIn(booking._id)" type="submit" value="Check In"></td>
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
    },

    checkIn(id){
      HotelService.updateBooking(id, { checked_in: true });
      this.bookings.find((booking) => {
        booking._id === id
        booking.checked_in = true
      })
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
