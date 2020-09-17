<template>
  <div>
    <div>
      <form class="homeText">
        <table>
        <tr>
          <td>Tapahtuma</td>
          <td><input id="name" v-model="eventName" placeholder="Luento" v-on:keydown="resetMessages()"></td>
        </tr>
          <tr>
        <td>Aika</td>
            <td><input id="time" v-model="eventTime" placeholder="30.10.2020" v-on:keydown="resetMessages()"></td>
          </tr>
          <tr>
            <td>Tapahtuma on tärkeä: <input type="checkbox" id="eventImportant" v-model="checked" v-on:click="resetMessages()"></td>
            <td><input type="submit" value="Lähetä" v-on:click="sendEvent()"></td>
          </tr>

        </table>
      </form>
    </div>
    <br>
    <h2 v-if="error" style="color:darkred">
      {{message}}
    </h2>
    <h2 v-else-if="success" style="color:green">
      {{message}}
    </h2>
  </div>
</template>
<script>
    import axios from 'axios';
    export default {
      name: 'AddEvent',
      data(){
        return {
          eventName: "",
          eventTime: "",
          checked: false,
          success: false,
          error: false,
        }

      },
      computed: {
        message: function(){
          if (this.success){
            document.getElementById("name").focus();
            return "Tiedot lähetetty!"
          } else if (this.error){
           return "Täytä kaikki kentät!"
          }else{
            return "";
          }
        }

      },
      methods: {
        sendEvent(){
          if (this.eventName == "" || this.eventTime == ""){
            this.error = true;
          }else {
            axios.post(`http://localhost:3001/events`, {
              content: this.eventName,
              date: this.eventTime,
              important: this.checked
            })

            this.eventName = "";
            this.eventTime = "";
            this.checked = false;
            this.success = true;
            this.error = false;
          }

        },
        resetMessages(){
          this.error = false;
          this.success = false;        }
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