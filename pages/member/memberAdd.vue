<script setup lang="ts">
import type { Member } from "@/interfaces";

const PAGE_TITLE = "会員情報追加";

definePageMeta({
  layout: "member",
});

useHead({
  title: PAGE_TITLE,
});

// ルーターオブジェクトを取得
const router = useRouter();
// 会員情報リストをステートから取得
const memberList = useState<Map<number, Member>>("memberList");
// 入力データと同期させるMemberオブジェクトの用意
const member: Member = reactive({
  id: 0,
  name: "",
  email: "",
  points: 0,
  note: "",
});
// フォームがサブミットされた時の処理
const onAdd = (): void => {
  memberList.value.set(member.id, member);
  router.push({ name: "member-memberList" });
};
</script>

<template>
  <nav id="breadcrumbs">
    <ul>
      <li><NuxtLink v-bind:to="{ name: 'index' }">TOP</NuxtLink></li>
      <li>
        <NuxtLink v-bind:to="{ name: 'member-memberList' }"
          >会員リスト</NuxtLink
        >
      </li>
      <li>{{ PAGE_TITLE }}</li>
    </ul>
  </nav>
  <section>
    <h2>{{ PAGE_TITLE }}</h2>
    <p>情報を入力し、登録ボタンをクリックしてください。</p>
    <form v-on:submit.prevent="onAdd">
      <dl>
        <dt>
          <label for="addId">ID&nbsp;</label>
        </dt>
        <dd>
          <input type="number" id="addId" v-model.number="member.id" required />
        </dd>
        <dt>
          <label for="addName">名前&nbsp;</label>
        </dt>
        <dd>
          <input
            type="text"
            id="addName"
            v-model.number="member.name"
            required
          />
        </dd>
        <dt>
          <label for="addEmail">メールアドレス&nbsp;</label>
        </dt>
        <dd>
          <input
            type="email"
            id="addEmail"
            v-model.number="member.email"
            required
          />
        </dd>
        <dt>
          <label for="addPoints">保有ポイント&nbsp;</label>
        </dt>
        <dd>
          <input
            type="number"
            id="addPoints"
            v-model.number="member.points"
            required
          />
        </dd>
        <dt>
          <label for="addNote">備考&nbsp;</label>
        </dt>
        <dd>
          <textarea id="addNote" v-model.number="member.note"></textarea>
        </dd>
        <button type="submit">登録</button>
      </dl>
    </form>
  </section>
</template>
