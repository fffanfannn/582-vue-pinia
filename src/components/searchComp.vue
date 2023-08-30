<template>
  <div>
    <h4>searchComp.vue</h4>
    <form action="">
      <input type="text" v-model="searchInput" id="name" name="name" />
      <button type="submit" @click="submitSearch">Search</button>
    </form>
    <button>close</button>

    <div v-if="searchInput">
      <div v-for="item in searchResults" :key="item._id">
        <p>{{ item.name }}</p>
        <p>{{ item.age }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { useOnlineStore } from "@/store/online";
import { useCodeSpacesStore } from "@/store/codespaceURL";
export default {
  name: "EditComp",
  setup() {
    const online = useOnlineStore();
    const codespaces = useCodeSpacesStore();
    return { online, codespaces };
  },
  props: {
    userData: Object,
  },

  data() {
    return {
      searchInput: "",
      searchResults: [],
    };
  },
  methods: {
    submitSearch(e) {
      e.preventDefault();
      this.searchResults = [];
      const form = document.querySelector("form");
      console.log(form);
      console.log(this.searchInput);
      console.log("online.user", this.online.users);
      for (let user of this.online.users) {
        if (user.name == this.searchInput) {
          console.log(user);
          this.searchResults.push(user);
          console.log(this.searchResults);
        }
      }
    },
  },
};
</script>
