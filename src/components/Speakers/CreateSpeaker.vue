<template>
  <div>
    <h1>Create speaker</h1>
    <form v-on:submit.prevent="createSpeaker">
      <p>model: <input type="text" v-model="speaker.model" /></p>
      <p>watt: <input type="text" v-model="speaker.watt" /></p>
      <p>power_input: <input type="text" v-model="speaker.power_input" /></p>
      <p>status: <input type="text" v-model="speaker.status" /></p>
      <p>stype: <input type="text" v-model="speaker.type" /></p>
      <p><button type="submit">create speaker</button></p>
    </form>
    <hr />
    <div>
      <p>model: {{ speaker.model}}</p>
      <p>watt: {{ speaker.watt }}</p>
      <p>power_input: {{ speaker.power_input }}</p>
      <p>status: {{ speaker.status }}</p>
      <p>status: {{ speaker.type }}</p>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";
export default {
  data() {
    return {
      speaker: {
        model: "",
        watt: "",
        power_input: "",
        status: "",
        type: ""
      }
    };
  },
  methods: {
    async createSpeaker() {
      try {
        await UsersService.post(this.speaker);
        this.$router.push({
          name: "speakers"
        });
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>
<style scoped></style>
