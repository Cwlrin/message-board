<template>
  <form action="" class="grid" @submit="handleSubmit">
    <textarea id="" v-model="content" class="bg-gray-50 p-2 rounded" name="comment" placeholder="请输入你的评论"></textarea>
    <fieldset class="py-4">
      <input class="px-4 py-1 bg-blue-600 rounded text-white" type="submit" value="评论"/>
      <input class="px-4 py-1 bg-white rounded border ml-3" type="reset" value="取消"/>
    </fieldset>
  </form>
</template>

<script setup>
import {ref} from "vue";

const content = ref("");

const emit = defineEmits(["submit"]);

const handleSubmit = (e) => {
  e.preventDefault();
  emit("submit", content.value);
  content.value = "";
};
</script>

<style scoped>

</style>