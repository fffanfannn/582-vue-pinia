<template>
  <section>
    <aside>Main page: sidebar<SideBarComp /></aside>
    <div>
      <header>Main page: header <HeaderComp /></header>
      <main>main-part(router-view)<router-view></router-view></main>
    </div>
  </section>
</template>

<script>
import HeaderComp from "@/components/HeaderComp.vue";
import SideBarComp from "@/components/SideBarComp.vue";

export default {
  name: "MainView",
  components: {
    SideBarComp,
    HeaderComp,
  },
};
</script>

<style scoped>
section {
  display: flex;
  height: 100vh;
}
aside {
  width: 30%;
  background-color: rgb(229, 241, 241);
}
div {
  width: 70%;
}
header {
  background-color: rgb(214, 230, 230);
}
</style>
