<template>
  <div>
    <h1>This is an account list page</h1>
  </div>
  <button @click="addBtn">create</button>
  <button @click="searchBtn">search</button>
  <ul>
    <li v-for="user in online.users" :key="user.id">
      <div id="name">{{ user.name }}</div>
      <div id="age">{{ user.age }}</div>
      <button :id="user._id" @click="editBtn">update</button>
      <button :id="user._id" @click="submitDelete">delete</button>
      <button :id="user._id" @click="submitDetail">details</button>
    </li>
  </ul>
  <DialogComp v-show="createDialog"></DialogComp>
  <EditComp v-show="editDialog" :userData="userData"></EditComp>
  <DetailsComp v-show="detailsDialog"></DetailsComp>
</template>

<script>
import { useOnlineStore } from "@/store/online";
import { useCodeSpacesStore } from "@/store/codespaceURL";
import DialogComp from "@/components/DialogComp.vue";
import EditComp from "@/components/EditComp.vue";
import DetailsComp from "@/components/DetailsComp.vue";
export default {
  name: "HeaderComp",
  setup() {
    const online = useOnlineStore();
    const codespaces = useCodeSpacesStore();
    return { online, codespaces };
  },

  data() {
    return {
      createDialog: false,
      editDialog: false,
      detailsDialog: false,
      userData: {
        name: "",
        age: "",
      },
    };
  },

  components: {
    DialogComp,
    EditComp,
    DetailsComp,
  },

  methods: {
    addBtn() {
      this.createDialog = !this.createDialog;
    },

    editBtn(event) {
      this.editDialog = !this.editDialog;
      this.userData = this.online.users.find(
        (user) => user._id === event.target.id
      );
      console.log(this.userData);
    },

    async submitDelete(e) {
      console.log(e.target.id);
      const codespaces = useCodeSpacesStore();
      await fetch(`${codespaces.csURL}api/account/delete/${e.target.id}`, {
        method: "delete",
      })
        .then((res) => {
          console.log(res);
          // return res.text();
        })
        .then((data) => {
          console.log(data);
        });

      // this.$router.push({ name: "Userlist" });
      location.reload();
    },

    submitDetail(e) {
      console.log(e.target.id);
      const codespaces = useCodeSpacesStore();
      fetch(`${codespaces.csURL}api/account/${e.target.id}`)
        .then((res) => {
          console.log(res);
          return res.text();
        })
        .then((data) => {
          console.log(data);
        });

      this.detailsDialog = !this.detailsDialog;
    },
  },

  created() {
    console.log("11");
    const codespaces = useCodeSpacesStore();
    fetch(`${codespaces.csURL}api/account/list`)
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
