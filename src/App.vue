<template>
  <v-app id="app" :style="{'background-image':`url(${backgroundUrl})`,backgroundPosition:'right'}">
      <v-row no-gutters v-if="loggedIn">
      <v-col :cols="barCols">
          <NavBar @pageChanged="currentPage = $event" @expanded="barCols=2" @retracted="barCols=1"/>
      </v-col>
        <v-col :cols="12 - barCols">
            <component :is='currentPage'/>
        </v-col>
      </v-row>
      <v-row no-gutters v-else>
          <v-col cols="12">
              <LogIn @logIn="onLogin" :wrong-user-name-password="wrongUserNamePassword"/>
          </v-col>
      </v-row>
  </v-app>
</template>

<script>
import LogIn from './components/LogIn';
import NavBar from "@/components/NavBar";
import Dash from "@/components/Dash";
import axios from 'axios';
import backgroundUrl from "@/assets/background.jpg"

export default {
  name: 'App',

  components: {
      Dash,
    LogIn,
    NavBar
  },
  data: () => ({
        a:false,
        wrongUserNamePassword: false,
        currentPage:null,
        barCols:1,
        backgroundUrl
  }),
    computed:{
        loggedIn:function () {
            return this.$cookies.isKey("apiKey");
        }
    },
    watchers:{
    },
    methods:{
      onLogin:function (userName,password) {
          let model = this;
            axios.get('/subject/logIn',{
                params:{
                    name:userName,
                    password:password
                }
                // eslint-disable-next-line no-unused-vars
            }).then(function (response) {
                model.wrongUserNamePassword = false;
                model.$cookies.set("apiKey",response.data);
                window.location.reload()
                // eslint-disable-next-line no-unused-vars
            }).catch(function (error) {
                model.wrongUserNamePassword = true;
            })
      }
    }
};
</script>

<style scoped>
    @import "fonts/fonts.css";
    #app{
        font-family: PingFang;
    }
</style>
