<template>
  <div>
    <h1>Show Speaker</h1>
    <p>model : {{ speaker.model }}</p>
    <p>watt :{{ speaker.watt }}</p>
    <p>power input : {{ speaker.power_input }}</p>
    <p>status : {{ speaker.status }}</p>
    <p>type : {{ speaker.type }}</p>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";
export default {
  data() {
    return {
      speaker: null
    };
  },
  async created() {
    let speakerId = this.$route.params.speakerId;
    this.speaker = (await UsersService.show(speakerId)).data;
  }
};
</script>
<style scoped></style>
