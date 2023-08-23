<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>{{ counter.count }}</p>
    <button @click="counter.increment()">Add</button>
    <button @click="counter.decrement()">Remove</button>
    <button @click="custom">Custom</button>
    <h2>Students</h2>
    <p>{{ school.students }}</p>
    <ul>
      <li
        @click="school.addStudent(student)"
        v-for="student in students"
        :key="student.id"
      >
        {{ student.name }} - {{ student.age }}
      </li>
    </ul>
    <h2>Teachers</h2>
    <p>{{ school.teachers }}</p>
    <ul>
      <li
        @click="school.addTeacher(teacher)"
        v-for="teacher in teachers"
        :key="teacher.id"
      >
        {{ teacher.name }} - {{ teacher.age }}
      </li>
    </ul>
    <h2>Users</h2>
    <!-- <p>{{ online.users }}</p> -->
    <ul>
      <li v-for="user in online.users" :key="user.id">{{ user.name }}</li>
    </ul>
  </div>

  <!-- <form
    action="https://friendly-carnival-qr7rxj6j4gw39q49-3000.app.github.dev/"
    method="post"
  >
    <label for="name"></label>
    <input type="text" name="name" v-model="user.name" />
    <button type="submit" @click="addAPI">send</button>
  </form> -->
  <form>
    <input type="text" id="name" name="name" placeholder="Name" />
    <input type="text" id="age" name="age" placeholder="Age" />
    <button type="submit" @click="testAPI">Submit</button>
  </form>
</template>

<script>
import { useCounterStore } from "@/store/counter";
import { useSchoolStore } from "@/store/school";
import { useOnlineStore } from "@/store/online";

export default {
  name: "AboutView",
  setup() {
    const counter = useCounterStore();
    const school = useSchoolStore();
    const online = useOnlineStore();
    return { counter, school, online };
  },
  data() {
    return {
      students: [
        { id: 1, name: "John", age: 18 },
        { id: 2, name: "Jane", age: 19 },
        { id: 3, name: "Joe", age: 20 },
      ],
      teachers: [
        { id: 1, name: "Mr. Smith", age: 40 },
        { id: 2, name: "Mrs. Smith", age: 39 },
        { id: 3, name: "Mr. Doe", age: 41 },
      ],
      user: {
        name: "",
      },
    };
  },
  methods: {
    custom() {
      console.log("custom");
      this.counter.increment();
    },
    // addAPI(e) {
    //   e.preventDefault();
    //   console.log("addAPI");
    //   fetch("https://friendly-carnival-qr7rxj6j4gw39q49-3000.app.github.dev/", {
    //     method: "POST",
    //     headers: {
    //       "Content-Type": "application/json",
    //     },
    //     body: JSON.stringify(this.user),
    //   });
    //   // .then((response) => response.json())
    //   // .then((json) => {
    //   //   console.log(json);
    //   //   this.online.addUser(json);
    //   // });
    // },

    testAPI() {
      const form = document.querySelector("form");
      form.addEventListener("submit", (e) => {
        e.preventDefault();
        let name = document.querySelector("#name").value;
        let age = document.querySelector("#age").value;
        const formData = { name, age };
        fetch(
          "https://friendly-carnival-qr7rxj6j4gw39q49-3000.app.github.dev/",
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
            return res.text();
          })
          .then((data) => {
            console.log(data);
          });
      });
    },
  },
  created() {
    fetch("https://friendly-carnival-qr7rxj6j4gw39q49-3000.app.github.dev/")
      .then((response) => response.json())
      .then((json) => {
        console.log(json);
        for (let user of json) {
          this.online.addUser(user);
        }
      });
  },
};
</script>
