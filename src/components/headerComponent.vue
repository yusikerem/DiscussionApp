<template>
  <div>
    <ul class="flex space-x-4 text-center fixed items-center w-full bg-white h-20">
       
      <li><router-link  v-if="!user" to="/" tag="a">Log-in</router-link></li>
      
      <li><router-link to="/discussions" tag="a">All Discussions</router-link></li>
      <hr />
      <li>
        <router-link v-if="!user" to="/register" tag="a">Register</router-link>
      </li>
      <hr>
      <li>
        <router-link @click.native="logOut" v-if="user" to="/register" tag="a"
          >Log-Out</router-link
        >
      </li>
      <div v-if="user" class="absolute right-4 ">
        Current user : {{user.email}}
      </div>
    </ul>
  </div>
</template>
<script>
import firebase from "firebase";
export default {
  data() {
    return {
      user: null,
    };
  },
  created() {
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.user = user;
      } else {
        this.user = null;
      }
    });
  },
  methods: {
    logOut() {
      firebase.auth().signOut();
    },
  },
};
</script>
