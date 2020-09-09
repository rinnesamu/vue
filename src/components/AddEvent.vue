<template>
    <p class="homeText">
        Syötä tapahtuma <br>
    </p>

</template>
<template>
  <form class="homeText">
    <table>
    <tr>
      <td>Tapahtuma</td>
      <td><input v-model="eventName" placeholder="Luento"></td>
    </tr>
      <tr>
    <td>Aika</td>
        <td><input v-model="eventTime" placeholder="30.10.2020"></td>
      </tr>
      <tr>
        <td>Tapahtuma on tärkeä: <input type="checkbox" id="eventImportant" v-model="checked"></td>
        <td><input type="submit" value="Lähetä" v-on:click="sendEvent()"></td>
      </tr>

    </table>
  </form>
</template>
<script>
    import axios from 'axios';
    export default {
      name: 'AddEvent',
      data(){
        return {
          eventName: null,
          eventTime: null,
          checked: false
        }

      },
      methods: {
        sendEvent(){
          axios.post(`http://localhost:3001/events`, {
            content: this.eventName,
            date: this.eventTime,
            important: this.checked
          })
          this.eventName = null;
          this.eventTime = null;
          this.checked = false;
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