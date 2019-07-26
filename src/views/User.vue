<template>
  <div class="user">
    <h1>This is a user page</h1>
    <v-app>
      <v-content>
        <div v-for="(user, i) in users"
          v-bind:key="i">
          <v-avatar>
            <img
              v-bind:src="user.picture.thumbnail"
              alt="John"
            >
          </v-avatar>
          <span>
            {{ user.name.first }}
          </span>
        </div>
      </v-content>
    </v-app>
  </div>
</template>

<script>
export default {
  name: 'user',
  data: function() {
    return {
      users: []
    };
  },
  created: function() {
    var self = this;
    axios.get('https://randomuser.me/api/?results=10')
      .then(function (response) {
        console.log(response);
        self.users = response.data.results;
      });
  }
}
</script>
