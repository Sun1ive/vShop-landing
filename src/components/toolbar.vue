<template>
  <div>
    <v-navigation-drawer right temporary v-model="drawer">
      <v-list class="pa-1">
        <v-list-tile avatar class="text-xs-center">
          <img src="/static/logo1.png">
        </v-list-tile>
      </v-list>
      <v-list class="pt-0">
        <v-divider></v-divider>
        <v-list-tile v-for="item in toolbar" :key="item.title" @click="">
          <v-list-tile-action>
            <v-icon medium class="red--text">{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content @click.stop="drawer = false" v-scroll-to="item.scroll">
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon medium class="red--text">menu</v-icon>
          </v-list-tile-action>
          <v-list-tile-content @click.stop="drawer = false">
            <v-list-tile-title>Свернуть</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar>
      <v-toolbar-title v-scroll-to="'.header'"><img class="logo" src="/static/logo1.png" alt="logo"></v-toolbar-title>
      <v-spacer></v-spacer>
        <v-btn flat class="request hidden-xs-only" @click.stop="requestConsult">Заказать звонок</v-btn>
      <!-- <v-toolbar-items class="dFlex hidden-xs-only" v-if="showNumbers">
          <v-icon medium class="red--text mx-2">call</v-icon><a href="tel:3336621">068-02-02-092</a>
          <v-icon medium class="red--text mx-2">call</v-icon><a href="tel:3336621">073-02-02-090</a>
      </v-toolbar-items> -->
      <v-spacer></v-spacer>
      <v-toolbar-side-icon class="hidden-lg-and-up" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-items class="hidden-md-and-down" v-for="(item, i) in toolbar" :key="i">
        <v-btn flat v-scroll-to="item.scroll" class="myBtn">{{ item.title }}</v-btn>
      </v-toolbar-items>
    </v-toolbar>
  </div>
</template>


<script>
import toolbarList from './toolbarList'

export default {
  props: ['showNumbers'],
  data() {
    return {
      drawer: null,
    }
  },
  methods: {
    showCallForm () {
      this.$emit('showCallForm')
    },
    requestConsult () {
      this.$emit('requestConsult')
    }
  },
  computed: {
    toolbar () {
      return toolbarList
    }
  }
}
</script>

<style scoped lang="stylus">
.logo
  cursor: pointer;

.dFlex
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 17px;
  font-weight: 600;
  a
    color: #333;

.myBtn
  // font-weight bold

.request
  background-color #F44336 !important
  color #fff !important
  // font-weight bold
  border-radius 6px

// .toolbar {
//   /* background: url('/static/grunde.png') center center repeat; */
// }
</style>