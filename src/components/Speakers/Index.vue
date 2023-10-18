<template>
  <div>
    <h2>Get all Speakers</h2>
    <h4>จำนวนลำโพง{{ speakers.length }}</h4>
    <div v-for="speaker in speakers" v-bind:key="speaker.id">
      <p>model : {{ speaker.model }}</p>
      <p>watt :{{ speaker.watt }}</p>
      <p>power input : {{ speaker.power_input }}</p>
      <p>status : {{ speaker.status }}</p>
      <p>type : {{ speaker.type }}</p>

      <p>
        <button v-on:click="navigateTo('/speaker/' + speaker.id)">
          ดูข้อมูลลำโพง
        </button>
      </p>
      <p>
        <button v-on:click="navigateTo('/speaker/edit/' + speaker.id)">
          แก้ไขข้อมูลลำโพง
        </button>
      </p>
      <p><button v-on:click="deleteSpeaker(speaker)">ลบข้อมูล</button></p>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      speakers: []
    };
  },
  async created() {
    this.speakers = (await UsersService.index()).data;
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteSpeaker(speaker) {
      try {
        await UsersService.delete(speaker);
        this.refreshData();
      } catch (err) {
        console.log(err);
      }
    },
    async refreshData() {
      this.speakers = (await UsersService.index()).data;
    }
  }
};
</script>
<style scoped></style>
