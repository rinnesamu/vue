<template>
  <p class="homeText">
    Tapahtumat: <br>
    <b-table :items = "data"></b-table>
  </p>

</template>
<script>


import axios from 'axios';

export default {
  name: 'ListEvent',
  data() {
    return {
      data: []
    }
  },
  beforeMount(){
    this.getEvents();
  },
  methods: {
    async getEvents(){
      const promise = axios.get('http://localhost:3001/events');
      promise.then(response => {
        //console.log("GET, response ", response.status, response.data);
        //console.log(response.data);
        this.data = response.data;
      })
    }
  }
};
</script>
<style scoped>
.homeText{
  font-size: 35px;
  color: red;
  text-align: center;
  position: relative;
  top:30px;
  text-shadow: 2px 2px 2px gray;
}
</style>