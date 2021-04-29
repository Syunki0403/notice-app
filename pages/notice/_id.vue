<template>
  <div class="w-full md:max-w-3xl mx-auto pt-20">
    <h2 class="text-xl pb-5 border-b border-gray-500 border-solid font-bold">
      {{ item.title }}
    </h2>
    <div class="pt-4 mb-4">
      <time class="text-gray-700 text-base">{{
        item.publishedAt | formatDate
      }}</time>
    </div>
    <div class="mb-20" v-html="item.body"></div>
    <div class="mb-10 mx-auto text-center">
      <a
        href="/notice/"
        class="font-semibold md:text-lg xl:text-base px-4 md:px-5 xl:px-4 py-3 md:py-4 xl:py-3 leading-tight shadow-md rouded-lg bg-blue-100 hover:bg-gray-200 text-gray-800"
      >
        お知らせへ戻る
      </a>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  async asyncData({ $config, params, error }) {
    try {
      const { data } = await axios.get(
        `${$config.apiUrl}/notice/${params.id}`,
        {
          headers: { "X-API-KEY": $config.apiKey },
        }
      );
      return {
        item: data,
      };
    } catch (err) {
      error({
        errorCode: 404,
      });
    }
  },
  head() {
    return {
      title: this.item.title,
    };
  },
};
</script>