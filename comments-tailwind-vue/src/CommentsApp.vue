<template>
  <main class="p-4 bg-gray-50 min-h-screen">
    <div class="max-w-screen-xl mx-auto bg-white p-8 rounded-lg shadow-2xl">
      <h2 class="text-3xl my-6">评论</h2>
      <!-- 留言表单 -->
      <CommentBox @submit="addNewComment"/>
      <!-- 分隔线 -->
      <DividerHorizontal/>
      <div v-for="comment in comments" :key="comment.id">
        <!-- 单个留言 -->
        <CommentItem :avatar="comment.avatar" :content="comment.content" :time="comment.time" :user="comment.user"/>
        <!-- 回复列表 -->
        <ReplyContainer v-if="comment.replies">
          <!-- 回复 -->
          <CommentItem v-for="reply in comment.replies" :key="reply.id" :avatar="reply.avatar" :content="reply.content"
                       :time="reply.time"
                       :user="reply.user"/>
        </ReplyContainer>
        <ReplyBox @submit="addNewComment($event, comment.id)"/>
      </div>
    </div>
  </main>
</template>

<script setup>
import CommentBox from "./components/CommentBox.vue";
import DividerHorizontal from "./components/DividerHorizontal.vue";
import CommentItem from "./components/CommentItem.vue";
import ReplyBox from "./components/ReplyBox.vue";
import ReplyContainer from "./components/ReplyContainer.vue";

import {ref, onMounted} from "vue";

const comments = ref([]);

async function getAllComments() {
  const res = await fetch("/api/comments");
  comments.value = await res.json();
}

onMounted(() => {
  getAllComments();
});

const addNewComment = async (content, replyTo) => {
  await fetch(`/api/comments`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      content,
      ...(replyTo && {replyTo}),
    }),
  });

  // 新增完评论后，自动获取新的评论列表
  // Notion API 有延迟，在添加完 page 之后，需要过一会才能获取到新的评论列表
  setTimeout(async () => {
    await getAllComments();
  }, 1000);
};
</script>

<style scoped>

</style>