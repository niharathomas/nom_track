<template>
  <div>
    <h1>Nom Track</h1>
    <h4>Your one stop shop for everything lunch around the Howard Hughes Center in Los Angeles</h4>
    <div class="text-danger">You have xx mins to get food... gogogo</div>
    <div class="text-warning">{{ now }}</div>
    <div class="mt-5 mb-5">
      <b-card-group deck class="mb-3 mx-auto d-flex justify-content-center">

    <div v-for="foodOption in todaysFoodOptions">
      <b-card :title="foodOption.name"
              img-src="https://lorempixel.com/600/300/food/5/"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width: 20rem;"
              class="mb-2">
        <div class="card-text">
          {{ foodOption.yelp_info.cost }}
        </div>
        <div v-if="foodOption.yelp_info.rating" class="card-text">
          Yelp Rating: {{ foodOption.yelp_info.rating }}
        </div>
        <b-button :href="foodOption.menu" variant="primary">Menu</b-button>
        <em slot="footer"> Location: {{ foodOption.type }}</em>
      </b-card>
    </div>
    </b-card-group>
    </div>

    <button @click="getTodaysFoodOptions">What should I eat today?</button>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        todaysFoodOptions: this.getTodaysFoodOptionsFromAPI(),
        now: new Date()
      }
    },
    methods: {
//      created () {
//        setInterval(() => this.now = new Date, 1000 * 60)
//      },
      getFoodImage () {
        const path = `https://lorempixel.com/600/300/food/`
        axios.get(path)
          .then(response => {
            console.log('Food Image ====')
            console.log(response)
            this.foodImage = response
          })
          .catch(error => {
            console.log('ERROR!!!!!!!!!!!')
            console.log(error)
          })
      },
      getTodaysFoodOptions () {
        this.todaysFoodOptions = this.getTodaysFoodOptionsFromAPI()
      },
      getTodaysFoodOptionsFromAPI () {
        const path = `http://localhost:5000/api/today`
        axios.get(path)
          .then(response => {
            this.todaysFoodOptions = response.data
          })
          .catch(error => {
            console.log('ERROR!!!!!!!!!!!')
            console.log(error)
          })
      }
    }
  }
</script>
