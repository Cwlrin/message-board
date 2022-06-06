<template>
  <main class="p-4 bg-gray-50 min-h-screen">
    <div class="max-w-screen-xl mx-auto bg-white p-8 rounded-lg shadow-2xl">
      <h2 class="text-3xl my-6">评论</h2>
      <!-- 留言表单 -->
      <CommentBox/>
      <!-- 分隔线 -->
      <DividerHorizontal/>
      <div v-for="comment in comments" :key="comment.id">
        <!-- 单个留言 -->
        <CommentItem :avatar="comment.avatar" :content="comment.content" :time="comment.time" :user="comment.user"/>
        <!-- 回复列表 -->
        <ReplyBox v-if="comment.replies">
          <!-- 回复 -->
          <CommentItem v-for="reply in comment.replies" :key="reply.id" :avatar="reply.avatar" :content="reply.content"
                       :time="reply.time"
                       :user="reply.user"/>
        </ReplyBox>
      </div>
    </div>
  </main>
</template>

<script setup>
import CommentBox from "./components/CommentBox.vue";
import DividerHorizontal from "./components/DividerHorizontal.vue";
import CommentItem from "./components/CommentItem.vue";
import ReplyBox from "./components/ReplyBox.vue";

import face1 from "./assets/嘉然今天吃什么.jpg";
import face2 from "./assets/珈乐Caral.jpg";
import face3 from "./assets/嘉心糖3.0.jpg";

const comments = [
  {
    id: 1,
    user: "梦落轻寻",
    avatar: face1,
    time: "2小时之前",
    content:
        "哇！这篇文章真是写的太好啦！收到很大的启发，希望博主能够再接再厉，产出越来越多，越来越好的文章！凑字数，字数，字数...",
    replies: [
      {
        id: 2,
        user: "陌上花开",
        avatar: face2,
        time: "2小时之前",
        content: "赞！",
      },
      {
        id: 3,
        user: "半梦半醒半浮生√<",
        avatar: face3,
        time: "2小时之前",
        content:
            "这是一篇非常长的长篇大论，这篇文章写的非常好，无论是技术点还是理论点，都非常的好。而且主题分明，每一个点都有自己的解释，这篇文章的主题是：CSS3的新特性，如何使用CSS3的新特性，以及如何使用CSS3的新特性。真的是非常好的文章。",
      },
    ],
  },
];
</script>

<style scoped>

</style>