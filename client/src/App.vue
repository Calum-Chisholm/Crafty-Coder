<template lang="html">
<div class="">
  <booking-form></booking-form>
  <guest-table></guest-table>
</div>
</template>

<script>
import BookingForm from '@/components/BookingForm';
import GuestTable from '@/components/GuestTable';

export default {
  name: 'app',
  components: {
    'booking-form': BookingForm,
    'guest-table': GuestTable
  }
}
</script>

<style lang="css" scoped>
</style>
