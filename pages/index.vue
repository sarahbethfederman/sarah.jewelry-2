<template>
  <div class="columns is-mobile is-multiline is-centered">
    <div class="column is-one-third-desktop" v-for="p in products">
      <small-product :product="p" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import SmallProduct from '~/components/SmallProduct.vue'

export default {
  components: {SmallProduct},
  async asyncData ({env, params}) {
    let {data} = await axios.get(`${env.cockpit.apiUrl}/collections/get/Product?token=${env.cockpit.apiToken}`)

    let products = data.entries.map((p) => {
      p.thumbUrl = `${env.cockpit.apiUrl}/${p.Image.path}`
      console.log(p)
      return p
    })

    return {
      products
    }
  }
}
</script>