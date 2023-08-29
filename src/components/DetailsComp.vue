<template>
  <div>
    <h4>Details items</h4>
  </div>
</template>

<script>
export default {
  name: "DetailsComp",
  methods: {
    submitCreate() {
      const form = document.querySelector("form");
      form.addEventListener("submit", (e) => {
        e.preventDefault();
        let name = document.querySelector("#name").value;
        let age = document.querySelector("#age").value;
        const formData = { name, age };
        fetch(
          "https://glowing-space-happiness-x65647x7qw4c6j4g-3000.app.github.dev/api/account/add",
          {
            method: "post",
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
};
</script>
