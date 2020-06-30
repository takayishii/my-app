<template>
  <div class="hello">
    <h1>{{ greet }}{{ msg }}</h1>
    <form @submit.prevent="onSubmit">
      <div class="form-group">
        <input id="word" v-model="word" type="text" placeholder="word" />
        {{ todoList }}
        <!-- <p class="error-msg" v-if="error">{{ error }}</p> -->
      </div>
      <!-- <button type="submit" @click="onClick">submit</button> -->
    </form>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class TakayaZone extends Vue {
  @Prop() private msg!: string;
  @Prop() private greet!: string;

  private todoList: string[] = [];
  private inputField = "";
  private baseUrl = "https://www.googleapis.com/youtube/v3/";

  public created() {
    this.getSearchResults();
  }
  private async getSearchResults() {
    try {
      const response = await axios.get(this.baseUrl + "search");
      this.todoList = response.data;
      return this.todoList;
    } catch (e) {
      return e;
    }
  }
}
</script>
