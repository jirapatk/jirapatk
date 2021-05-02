<template>
  <v-container>
    <div>
      <h1>{{ customer.cus_firstname }}</h1>
      <p> เบอร์โทรศัพท์ {{ customer.cus_phone }}</p>
    </div>
  </v-container>
</template>

<script>
export default {
  async asyncData ({ params, $axios }) {
    const customer = await $axios.$get(`customers/${params.id}`)
    return { customer }
  }
}
</script>
