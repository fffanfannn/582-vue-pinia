<template>
  <div>
    <h4>editComp.vue</h4>
    <form action="">
      <input type="text" id="name" name="name" placeholder="Name" />
      <input type="text" id="age" name="age" placeholder="Age" />
      <button type="submit" @click="editCreate">Edit</button>
    </form>
    <button>close</button>
  </div>
</template>

<script>
export default {
  name: "EditComp",
  props: {
    userData: Object,
  },
  methods: {
    editCreate() {
      const form = document.querySelector("form");
      form.addEventListener("submit", (e) => {
        e.preventDefault();
        let name = document.querySelector("#name").value;
        let age = document.querySelector("#age").value;
        const formData = { name, age };
        fetch(
          `https://glowing-space-happiness-x65647x7qw4c6j4g-3000.app.github.dev/api/account/${e.target.id}`,
          {
            method: "patch",
            body: JSON.stringify(formData),
            headers: {
              "Content-Type": "application/json",
              // 'Content-Type': 'application/x-www-form-urlencoded',
            },
          }
        )
          .then((res) => {
            console.log(res);
            alert("Account item created successfully");
            return res.text();
          })
          .then((data) => {
            console.log(data);
          });
      });
    },
  },
  created() {
    console.log(this.userData.name);
  },
};
</script>
