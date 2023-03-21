<script setup lang="ts">
import BlogPost from "./components/BlogPost.vue";
import ButtonCounter from "./components/ButtonCounter.vue";
import CustomInput from "./components/CustomInput.vue";
import SlotButton from "./components/SlotButton.vue";

const className = "class-variable";
const url = "https://www.naver.com";
</script>

<script lang="ts">
export default {
  components: {
    ButtonCounter,
    BlogPost,
    SlotButton,
  },
  data() {
    return {
      isActive: true,
      count: 1,
      author: {
        name: "John",
        books: ["Vue1", "Vue2", "Vue3"],
      },
      isAwesome: true,
      myObject: {
        title: "Vue 목록 작성",
        author: "나",
        publishDate: "2022-03-20",
      },
      message: "",
      posts: [
        { id: 1, title: "Post A" },
        { id: 2, title: "Post B" },
        { id: 3, title: "Post C" },
      ],
      firstName: "",
      lastName: "",
    };
  },
  //캐싱 사용, method로 구현보다 더 좋음
  //method로 구현 시 리렌더링마다 함수 실행됨
  computed: {
    hasBook() {
      return this.author.books.length > 0 ? "YES" : "NO";
    },
    computeIsActive() {
      return this.isActive ? "ACTIVE" : "NOT ACTIVE";
    },
    classObject() {
      return {
        active: this.isActive,
      };
    },
  },
  watch: {
    //isActive가 변경될 때마다 실행
    isActive: {
      handler(newIsActive, oldIsActive) {
        console.log(newIsActive, oldIsActive);
      },
      //원래 lazy, 최초 데이터 구성된 후 콜백이 실행되기를 바랄 경우 옵션
      immediate: true,

      //중첩된 모든 변경에 대해 콜백이 실행되도록 함
      deep: true,
    },
  },
  methods: {
    // 화살표 함수 사용 금지, this에 접근 불가
    increment() {
      this.count++;
    },
    toggleIsActive() {
      this.isActive = !this.isActive;
    },
    toggleIsAwesome() {
      this.isAwesome = !this.isAwesome;
    },
    test(arg: string, event: Event) {
      console.log(event.target);
      console.log(arg);
    },
  },
};
</script>

<template>
  <div id="app">
    <div>
      <span :class="className">class</span>
      <span>{{ className }}</span>

      <a :href="url">NAVER</a>
      <div v-if="isActive" :class="classObject">dynamic Visible</div>
      <div v-if="!isActive">dynamic NOT Visible</div>

      <button @click="toggleIsActive">{{ computeIsActive }}</button>

      <button @click="increment">Count ++</button>

      <p>count is {{ count }}</p>
      <p>has Book ? {{ hasBook }}</p>

      <button @click="toggleIsAwesome">Switch</button>

      <!-- 일반적으로 v-if는 전환 비용이 더 높고, v-show는 초기 렌더링 비용이 더 높습니다. 
      따라서 매우 자주 전환해야 하는 경우 v-show를, 
      실행 중에 조건이 변경되지 않는 경우 v-if를 사용하는 것이 좋습니다. -->
      <h1 v-if="isAwesome">Vue는 멋짐</h1>
      <h1 v-else>아님?</h1>

      <ul>
        <li v-for="(book, index) in author.books">
          {{ index }} th book : {{ book }}
        </li>
      </ul>

      <ul>
        <li v-for="(value, key, index) in myObject" :key="key">
          {{ index }}th => {{ key }} : {{ value }}
        </li>
      </ul>

      <button @click="(event) => test('aaa', event)">Method Test</button>

      <p>메세지 : {{ message }}</p>
      <input v-model="message" placeholder="메세지 입력" />

      <ButtonCounter title="BUTTON COUNTER" />
    </div>

    <div class="blog-container">
      <!-- 변수값 동적 할당 -->
      <!-- v-bind를 이용해서 javascript 라는 것을 알려줘야 함 -->
      <!-- fallthrough, class를 자식에서 지정하지 않았어도 자동으로 들어감 -->
      <BlogPost
        :initial-likes="2"
        v-for="post in posts"
        :key="post.id"
        :title="post.title"
        class="blog-post-content"
      />
    </div>
    <div>
      <CustomInput
        v-model:first-name="firstName"
        v-model:last-name="lastName"
      />

      <!-- slot자리에 들어가는 것 -->
      <SlotButton>
        <p>Button</p>
        <template #main="{ message }"> {{ message }} </template>
      </SlotButton>
    </div>
  </div>
</template>

<style>
.active {
  color: red;
}

#app {
  display: flex;
  flex-direction: row;
}
#app > div {
  width: 50%;
}

.blog-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 20px;
}
</style>
