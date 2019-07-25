<template>
  <div class="user">
    <h1>This is an user page</h1>
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
        self.users.push(response.data.results);
      });
  }
}
</script>
