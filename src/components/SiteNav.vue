<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="container">
      <div class="navbar-brand">
        <a
                href="#"
                class="navbar-item"
        >
          <span class="icon is-large">
            <span class="fa-stack fa-md">
                <i class="fas fa-fire fa-stack-2x has-text-black"></i>
            </span>
          </span>
          &nbsp;
          <h1 class="title is-3 is-fat is-uppercase has-text-danger">This is <span class="has-text-dark">SPARTA</span></h1>
        </a>

        <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start">
          <p class="navbar-item"></p>
          <a class="navbar-item" @click="changePage('game')">
            Game
          </a>
          <a class="navbar-item" @click="changePage('nft')">
            Wins
          </a>
          <a class="navbar-item" @click="changePage('about')">
            About
          </a>
        </div>

        <div class="navbar-end">
          <div class="navbar-item" v-if="isConnected">
            <a class="is-small has-text-danger" v-if="!rememberMe" @click="rememberMeLink">Remember Me</a>
            <p class="is-small" v-if="rememberMe">Welcome Back!</p>
          </div>
          <div class="navbar-item">
            <div class="buttons">
              <button
                      v-if="!isConnected"
                      @click="connectButton"
                      :disabled="connectDisabled"
                      class="button is-danger is-small">
                <span class="icon">
                  <i class="fab fa-ethereum"></i>
                </span>
                <span>Connect</span>
              </button>
            </div>
            <span v-if="isConnected" class="tag is-danger">{{account.substring(1,6)}}...</span>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>

export default {
  name: 'SiteNav',
  data: () => {
    return {
      connectDisabled: false,
      rememberMe: false
    }
  },
  props: {
    isConnected: Boolean,
    account: String,
    balance: String
  },
  mounted: function() {
    this.loadRememberMe();
  },
  methods: {
    connectButton: function() {
      this.connectDisabled = true;
      this.$emit('connect');
    },
    loadRememberMe: async function() {
      this.rememberMe = document.cookie;
      if(this.rememberMe) {
        this.connectDisabled = true;
        this.$emit('connect');
      }
    },
    rememberMeLink: async function() {
      this.rememberMe = true;
      document.cookie = "rememberMe=true";
    },
    changePage: function(page) {
      this.$emit('changePage', page);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .navbar {
    margin-bottom: 2em;
  }
  .is-small {
    font-size: 0.9em;
  }
</style>
