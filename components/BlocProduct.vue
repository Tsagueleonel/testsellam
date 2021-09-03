<template>
  <div>
    <p v-if="$fetchState.pending">
      <span class="loading"></span>
    </p>
    <p v-else-if="$fetchState.error">Error while fetching mountains 🤬</p>
    <div v-else>
      <div  v-for="product in products" :key="product.id" class="container mt-4">
        <b-card :img-src="product.image" :img-alt="product.title" img-right>
          <b-card-text>
            <h3>{{ product.title }}</h3>
            <br/>
            {{ product.description }}
            <br/>
            <br/>
            <div>
              <span class="price">{{ product.price }}</span>
              <span class="divid"> - </span>
              <span class="oldPrice">
                <strike>{{ product.oldPrice }}</strike>
              </span>
            </div>
            <div class=" container pt-2">
              <NuxtLink :to="{name:'tutorial', params: {id: product.id} }"><b-button block pill variant="outline-danger" size="sm">Acheter</b-button></NuxtLink>
            </div>
          </b-card-text>
        </b-card>
      </div>
<!--      <li v-for="product in products" :key="product.id">
        <NuxtLink
          :to="{ name: 'mountains-slug', params: { slug: product.slug } }"
        >
          {{ product.title }}
        </NuxtLink>
      </li>-->
      <div class="pt-5"></div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      products: []
    }
  },
  activated() {
    if (this.$fetchState.timestamp <= Date.now() - 30000) {
      this.$fetch()
    }
  },

  async fetch() {
    this.products = await fetch(
      'http://localhost:3000/data/products.json'
    ).then((res) => res.json())
  }
}
</script>

<style scoped>
.price{
  color: #007bff;
  font-weight: bold;
  font-size: 30px;
}
.oldPrice{
  color: #e02561;
  font-weight: bold;
  font-size: 15px;
}
.divid{
  color: #000;
  font-weight: bold;
  font-size: 30px;
}
img[data-v-54ecee34]{
  width: 300px;
}

a[data-v-54ecee34], a[data-v-54ecee34]:hover{
  text-decoration: none;
}
</style>
