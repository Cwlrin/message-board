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
        <ReplyBox @submit="addReply($event, comment.id)"/>
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

import face1 from "./assets/嘉然今天吃什么.jpg";
import face2 from "./assets/珈乐Caral.jpg";
import face3 from "./assets/嘉心糖3.0.jpg";
import face4 from "./assets/嘉心糖3.0.jpg";

import {ref} from "vue";

const comments = ref([
  {
    id: 1,
    user: "柯洁",
    avatar: face1,
    time: "昨天",
    content:
        "“本手”字面意思为本分的一手，常常形容在棋局当下选择中庸的一手，介于不坏和好之间，但中庸并不等同于“平庸”。" +
        "\n" +
        "“俗手”意为庸俗的一手 在绝大多数情况下为贬义，但在某些情况下俗手的交换反而有可能成为当下最好的选择。\n" +
        "\n" +
        "“妙手”意为卓越的一手，可遇不可求，其本身具有极强的隐蔽性和唯一性，在大多数对局中往往并不常见 ，很多人在对局中经常会过分拘泥于局部，下出“假妙手”而忽略全局思维的错误。想下出真正的“妙手”，必须在平日有一定的经验积累和训练才可能完成真正卓越的“妙手”\n" +
        "抛砖引玉👀下回考就知道该怎么写了",
    replies: [
      {
        id: 2,
        user: "33今天改什么",
        avatar: face2,
        time: "1小时之前",
        content: "我作文编了一句你没说过的话 你赶紧开播把这话说一下",
      },
      {
        id: 3,
        user: "吃冰冰的肖酱",
        avatar: face3,
        time: "12小时之前",
        content:
            "你是高考考上清华的吗？",
      },
      {
        id: 4,
        user: "染柳知许",
        avatar: face3,
        time: "44分钟之前",
        content:
            "我考试拿你当素材说你白天下百盘棋晚上读千遍谱，你能直播兑现一下吗",
      },
      {
        id: 5,
        user: "卡塔利纳的侯国玉",
        avatar: face3,
        time: "54分钟之前",
        content:
            "都不如欧内的手",
      },
    ],
  },
]);

let rid = ref(5);

const constructNewComment = (content) => {
  return {
    id: rid.value++,
    user: "当前用户",
    avatar: face4,
    content,
    time: "1秒前",
  };
};

const addNewComment = (content) => {
  const newComment = constructNewComment(content);
  comments.value.push(newComment);
};

const addReply = (content, id) => {
  const reply = constructNewComment(content);
  let comment = comments.value.find((comment) => comment.id === id);
  if (comment.replies) {
    comment.replies.push(reply);
  } else {
    comment.replies = [reply];
  }
};
</script>

<style scoped>

</style>