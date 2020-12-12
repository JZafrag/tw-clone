<template>
	<div class="user-profile">
        <div class="user-profile__user-panel">
			<h1 class="user-profile__username">@{{user.username}}</h1>
			<div class="user-profile__admin-badge">
                <div v-if="user.isAdmin == true" class="user-profile__admin-badge">
                    Admin
                </div>
			</div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong>{{ followers }}  
            </div>
        </div>
        <div class="user-profile__tweets-wrapper">
            <div
            class="user-profile__tweet"
            v-for="tweet in user.tweets"
            v-bind:key="tweet.id"
            >
                {{ tweet.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
	name: "UserProfile",
	data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "JosueZafra",
        firstName: "Josue",
        lastName: "Zafra",
        email: "joe@idk.com",
        isAdmin: true,
        tweets: [
            { id: 1, content: "Twitter is not amazing"},
            { id: 2, content: "Don't forget to..."},
        ],
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount)
        console.log(`${this.user.username} has gained a follower!`);
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUser() {
      this.followers++; 
    },
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

h1 {
  margin: 0;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
</style>