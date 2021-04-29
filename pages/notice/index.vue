<template>
  <div class="w-full md:max-w-3xl mx-auto pt-20">
    <h2 class="font-sans text-lg text-gray-800 text-center text-3xl mb-10">
      お知らせページ
    </h2>
    <div class="mb-20">
      <div v-for="(item, index) in items" :key="index" class="bg-yellow-100 border-t-4 border-yellow-500 rouded-b text-teal-900 shadow-md mb-5">
        <a :href="'/notice/' + item.id + '/'" class="block px-4 py-3">
          <time class="text-gray-700 text-base mb-1 block md:w-1/6">
            {{ item.publishedAt | formatDate }}
          </time>
          <div class="md:w-10/12">{{ item.title }}</div>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  async asyncData({ $config }) {
    const { data } = await axios.get(`${$config.apiUrl}/notice`, {
      headers: { "X-API-KEY": $config.apiKey },
    });
    return {
        items: data.contents
    }
  },
};
</script>