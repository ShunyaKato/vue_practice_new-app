<template>
  <div id="todo">
    <p>
      <input
        type="text"
        placeholder="TODOを入力しましょう！"
        v-model="newItemTitle"
        @keyup.enter="addTodo()"
      />
    </p>
    <button @click="deleteTodo()">チェック済みの項目を削除する</button>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <label :class="{deleteLine: item.isChecked}">
          <input type="checkbox" v-model="item.isChecked" />
          {{ item.title }}
        </label>
      </li>
    </ul>
  </div>
</template>

<script>
// えみちゃんの
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  // data() {
  //   return {
  //     items: [],
  //     newItemTitle: ""
  //   };
  // }
  items = [];
  newItemTitle = ""; // 上のdata書き換え

  mounted() {
    this.loadTodo();
  }
  addTodo() {
    this.items.unshift({
      title: this.newItemTitle,
      isChecked: false
    });
    this.newItemTitle = "";
    this.saveTodo();
  }
  deleteTodo() {
    this.items = this.items.filter(function(item) {
      return item.isChecked === false;
    });
    this.saveTodo();
  }
  saveTodo() {
    localStorage.setItem("items", JSON.stringify(this.items));
  }
  loadTodo() {
    this.items = JSON.parse(localStorage.getItem("items"));
    if (!this.items) {
      this.items = [];
    }
  }
}

// //しゅんちゃんの
// export default {
//   // el: "#todo",
//   data: {
//     items: [],
//     newItemTitle: ""
//   },
//   methods: {
//     addTodo() {
//       this.items.unshift({
//         title: this.newItemTitle,
//         isChecked: false
//       });
//       this.newItemTitle = "";
//       this.saveTodo();
//     },
//     deleteTodo() {
//       this.items = this.items.filter(function(item) {
//         return item.isChecked === false;
//       });
//       this.saveTodo();
//     },
//     saveTodo() {
//       localStorage.setItem("items", JSON.stringify(this.items));
//     },
//     loadTodo() {
//       this.items = JSON.parse(localStorage.getItem("items"));
//       if (!this.items) {
//         this.items = [];
//       }
//     }
//   },
//   mounted() {
//     this.loadTodo();
//   }
// };
</script>