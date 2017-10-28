<template>
  <div class="dashboard">
    <h1>{{ msg }}</h1>
    <div>
      <md-layout class="card">
      <md-layout></md-layout>
      <md-layout md-flex="50">
        <md-card md-with-hover>
          <md-card-content>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non, voluptas eius illo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi.
          </md-card-content>
          <md-card-actions>
            <md-button class="md-icon-button">
              <md-icon>favorite</md-icon>
            </md-button> 200
          </md-card-actions>
        </md-card>
      </md-layout>
      <md-layout></md-layout>
      </md-layout>
      <md-layout class="card">
      <md-layout></md-layout>
      <md-layout md-flex="50">
        <md-card md-with-hover>
          <md-card-content>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non, voluptas eius illo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi.
          </md-card-content>
          <md-card-actions>
            <md-button class="md-icon-button">
              <md-icon>favorite</md-icon>
            </md-button> 200
          </md-card-actions>
        </md-card>
      </md-layout>
      <md-layout></md-layout>
      </md-layout>
      <md-layout class="card">
      <md-layout></md-layout>
      <md-layout md-flex="50">
        <md-card md-with-hover>
          <md-card-content>
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non, voluptas eius illo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi.
          </md-card-content>
          <md-card-actions>
            <md-button class="md-icon-button">
              <md-icon>favorite</md-icon>
            </md-button> 200
          </md-card-actions>
        </md-card>
      </md-layout>
      <md-layout></md-layout>
      </md-layout>
    </div>
    <div v-if="userExists">
      Welcome {{ pseudo }}. Destroy your account by clicking <a href="#" @click="destroyAccount">here</a>.
    </div>
    <div v-else>Sign up <router-link to="/signup">here</router-link>.</div>
  </div>
</template>

<script>
import Users from '@/js/users'

export default {
  name: 'dashboard',
  data () {
    return {
      msg: 'Welcome to Automi',
      pseudo: undefined
    }
  },
  computed: {
    userExists: function () {
      return (typeof this.pseudo !== 'undefined')
    }
  },
  beforeCreate: function () {
    Users.init().then(() => {
      Users.exists(window.web3.eth.accounts[0]).then((exists) => {
        if (exists) {
          Users.authenticate().then(pseudo => {
            this.pseudo = pseudo
          })
        }
      })
    }).catch(err => {
      console.log(err)
    })
  },
  methods: {
    destroyAccount: function (e) {
      e.preventDefault()
      Users.destroy().then(() => {
        this.pseudo = undefined
      }).catch(err => {
        console.log(err)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  display: block;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.card {
  padding: 20px 0px;
}
</style>
