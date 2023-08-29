<template>
  <div>
    <h1>This is an account list page</h1>
  </div>
  <button @click="addBtn">create</button>
  <ul>
    <li v-for="user in online.users" :key="user.id">
      <div>{{ user.name }}</div>
      <div>{{ user.age }}</div>
      <button :id="user._id" @click="editBtn">update</button>
      <button :id="user._id" @click="submitDelete">delete</button>
    </li>
  </ul>
  <DialogComp v-show="createDialog"></DialogComp>
  <EditComp v-show="editDialog"></EditComp>
</template>

<script>
import { useOnlineStore } from "@/store/online";
import DialogComp from "@/components/DialogComp.vue";
import EditComp from "@/components/EditComp.vue";
export default {
  name: "HeaderComp",
  setup() {
    const online = useOnlineStore();
    return { online };
  },

  data() {
    return {
      createDialog: false,
      editDialog: false,
    };
  },

  components: {
    DialogComp,
    EditComp,
  },

  methods: {
    addBtn() {
      this.createDialog = !this.createDialog;
    },

    editBtn() {
      this.editDialog = !this.editDialog;
    },

    submitDelete(e) {
      console.log(e.target.id);
      fetch(
        `https://glowing-space-happiness-x65647x7qw4c6j4g-3000.app.github.dev/api/account/delete/${e.target.id}`,
        {
          method: "delete",
        }
      )
        .then((res) => {
          console.log(res);
          return res.text();
        })
        .then((data) => {
          console.log(data);
        });
    },
  },

  created() {
    console.log("11");
    fetch(
      "https://glowing-space-happiness-x65647x7qw4c6j4g-3000.app.github.dev/api/account/list"
    )
      .then((response) => response.json())
      .then((data) => {
        console.log("created() data:", data);
        for (let user of data) {
          this.online.addUser(user);
        }
      });
  },
};
</script>
