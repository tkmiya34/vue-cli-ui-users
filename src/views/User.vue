<template>
  <div class="user">
    <h1>This is a user page</h1>
    <v-app>
      <v-content>
        <v-form>
          <v-container grid-list-xl>
            <v-layout wrap>

              <v-flex xs12 sm6 md3>
                <v-text-field
                  label="Regular"
                  v-model='search_text'
                ></v-text-field>
              </v-flex>
            </v-layout>
          </v-container>
        </v-form>


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
import algoliasearch from 'algoliasearch';

export default {
  name: 'user',
  data: function() {
    return {
      search_text: '',
      users: [],
      index: null
    };
  },
  created: function() {
    var self = this;

    // Algolia APIクライアントを初期化
    var searchClient = algoliasearch(
      'APP_ID',
      'SECRET_KEY'
    )
    // 使用するindexを指定
    self.index = searchClient.initIndex('user');
    this.searchUser()
  },
  watch: {
    search_text: function () {
      this.searchUser()
    }
  },
  methods: {
    searchUser: function () {
      var self = this;
      // ここでAlgoliaのAPIへ検索リクエストを投げています
      // searchメソッドの第一引数が検索文字列です。
      // 試しに "art" で検索してみます
      self.index.search(self.search_text, (err, { hits } = {}) => {
        // 検索結果をデータバインドしているusersに格納
        self.users = hits;
      });
    }
  }
}
</script>

