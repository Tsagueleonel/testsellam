<template>
  <div >
      <div v-for="product in products" :key="product.id">
        <div v-if="product.id === id">
          <b-breadcrumb>
            <b-breadcrumb-item >
             <NuxtLink to="/"> <b-icon icon="house-fill" scale="1.25" shift-v="1.25" aria-hidden="true"></b-icon>
               Accueil</NuxtLink>
            </b-breadcrumb-item>
            <b-breadcrumb-item href="#">{{ product.title }}</b-breadcrumb-item>
          </b-breadcrumb>

          <div class="container">
            <b-row>
              <b-col cols="8">
                <b-card :img-src="product.image" :img-alt="product.title" img-top>
                  <b-card-text>
                    <p class="description">Description : </p>
                    {{ product.description }}
                  </b-card-text>
                </b-card>
              </b-col>
              <b-col cols="4">
                <div>
                  <h3>{{ product.title }}</h3>
                  <span v-for="tag in product.tag" :key="tag.title" class="mr-2 mt-2">
                    <b-button variant="outline-primary" size="sm" >{{ tag.title }}</b-button>
                  </span>
                  <div class="mt-3">
                    <span class="price">{{ product.price }}</span>
                    <span class="divid"> - </span>
                    <span class="oldPrice">
                      <strike>{{ product.oldPrice }}</strike>
                    </span>
                  </div>
                  <div class="mt-3">
                    <b-button v-b-toggle.sidebar-right pill block class="buy">Buy now</b-button>
                      <b-sidebar id="sidebar-right" title="" right shadow>
                        <div class="px-3 py-2">
                          <div>
                            <p class="text-center font-weight-bold size">Thank You !</p>
                          </div>
                          <hr class="under"/>
                          <p>
                            Thank you for purchasing <span style="font-weight: bold; font-size: 15px">{{product.title}}</span> for
                            <div class="text-center font-weight-bold" style="color: #e02561; font-size: 25px">{{product.price}}</div>
                            <div class="container">
                              <NuxtLink to="/"><b-button block pill variant="danger">Go to home</b-button></NuxtLink>
                            </div>
                          </p>
                        </div>
                      </b-sidebar>
                  </div>
                </div>
              </b-col>
            </b-row>
          </div>


        </div>
      </div>

  </div>

</template>

<script>
export default {
  name: "tutorial",
  data() {
    return {
      products: [],
      id: this.$route.params.id
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
.under{
  border-top: 2px solid rgb(0 0 0);
  width: 200px;
}
div{
  color:black
}
.description{
  font-weight: bold;
  color: black;
}
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
.buy{
  color:white;
  background-color:black;
}

.size{
  font-size:20px
}
a[data-v-a5608c52], a[data-v-a5608c52]:hover{
  text-decoration: none;
}
</style>
