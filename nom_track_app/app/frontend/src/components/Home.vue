<template>
  <div>
    <h1>Nom Truck</h1>
    <h4>Your one stop shop for everything lunch around the Howard Hughes Center in Los Angeles</h4>
    <!--<p>Response from /api/today: </p>-->
    <!--<div v-for="foodOption in todaysFoodOptions">-->
      <!--{{ foodOption }}-->
    <!--</div>-->
    <div><b-card-group deck>

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

    <button @click="getTodaysFoodOptions">What's for lunch?</button>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        todaysFoodOptions: this.getTodaysFoodOptionsFromAPI()
      }
    },
    methods: {
      getTodaysFoodOptions () {
        this.todaysFoodOptions = this.getTodaysFoodOptionsFromAPI()
      },
      getTodaysFoodOptionsFromAPI () {
        const path = `http://localhost:5000/api/today`
        axios.get(path)
          .then(response => {
            console.log(response.data)
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
