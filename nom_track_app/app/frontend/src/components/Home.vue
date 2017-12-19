<template>
  <div>
    <p>Home page</p>
    <p>Response from /api/today: </p>
    <div v-for="foodOption in todaysFoodOptions"> {{ foodOption }} </div>
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
