<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-count">
        <strong> Followers: </strong>{{ followers }}
      </div>
    </div>
    <div class="user-profile_twoots-wrapper">
        <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" @favourite="toggleFavourite"/>
        

    </div>

    <button @click="followUser">follow</button>
  </div>
</template>

<script>
import TwootItem from "./twootItem";

export default {
  name: "App",
  components:{ TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_principalkelvo",
        firstName: "Principal",
        lastName: "Kelvo",
        email: "principalkelvo@gmail.com",
        isAdmin: false,
        twoots:[
            {id: 1, content: "Twooter is Amazing!"},
            {id: 2, content: "Dont forget to subscribe"},
            {id: 3, content: "Welcome back!"}
        ]
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount > newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`added to favourite #${id}`)
    }
  },
  mounted(){
      this.followUser();
  }
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 3px solid #0FE3E8;
}

.user-profile_admin-badge{
    background-color: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1 {
  margin: 0;
}
</style>
