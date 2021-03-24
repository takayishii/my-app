<template>
  <div>
    <div>
      <table>
        <tr>
          <th>日付</th>
          <th>名前</th>
          <th>作業内容</th>
          <th>作業実績(min)</th>
          <th>作業結果</th>
          <th>redmine</th>
          <th>台帳番号</th>
          <th>その他番号</th>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
          <td></td>
        </tr>
      </table>
    </div>
    <div>
      <font size="6" color="#c71585">YouTube Search list (Vue.js CLI)</font>
    </div>
    <br />
    <div><input size="40" type="text" disabled v-model="baseUrl" /></div>
    <input size="40" v-model="keyword" placeholder="検索キーワードを入力" />
    <button @click="searchVideo">検索</button>
    <table cellspacing="0" cellpadding="5" v-show="results">
      <tr>
        <th width="50">
          <font>No</font>
        </th>
        <th width="200">
          <font>Video</font>
        </th>
        <th width="700">
          <font>Contents</font>
        </th>
      </tr>

      <tr v-for="(movie, index) in results" v-bind:key="movie.id.videoId">
        <!-- No -->
        <td valign="top" width="50">{{ index + 1 }}</td>
        <!-- Video -->
        <td valign="top" width="300">
          <a
            v-bind:href="'https://www.youtube.com/watch?v=' + movie.id.videoId"
          >
            <img
              width="300"
              height="200"
              v-bind:src="movie.snippet.thumbnails.medium.url"
            />
          </a>
        </td>
        <!-- titleとdescription -->
        <td align="left" valign="top" width="700">
          <font size="5" color="#c71585"
            ><b>{{ movie.snippet.title }}</b></font
          >
          <br />
          {{ movie.snippet.description }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import axios from "axios";
import Params from "../models/Params";
@Component
export default class DailyReport extends Vue {
  @Prop() msg!: string;

  baseUrl = "https://www.googleapis.com/youtube/v3";
  keyword = "nonkapibara";
  order = "viewCount"; // リソースを再生回数の多い順に並べます。
  params: Params = new Params();
  results: unknown = null;
  public searchVideo() {
    console.log("Hello!!");
    this.params.q = this.keyword;
    // const self = this;
    axios
      .get(this.baseUrl + "/search", {
        params: this.params,
      })
      .then((res) => {
        console.log(res);
        this.results = res.data.items;
      });
  }
}
</script>

<style></style>
