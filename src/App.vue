<template>
  <v-app>
  <v-container fluid pa-0 id= "container">

      <Sidebar v-on:switchRoute = "switchRoute"/>


      <template v-if="routes === 'Home'">
                <Content 
                v-on:viewDebt = "viewDebt"
                v-on:addNewDebtor = "addNewDebtor"
                :debtors = "debtor" />
      </template>
      <template v-if="routes === 'ViewDebt'">
                <ViewDebt :debtData = "debtData" />
      </template>



</v-container>
</v-app>
</template>

<script>
import Sidebar from "./components/Sidebar"
import Content from "./components/Content"
import ViewDebt from "./components/ViewDebt"
import DebbieForm from "./components/DebbieForm"

export default {
  name: 'App',
  components: {
    Sidebar, Content, ViewDebt, DebbieForm
  },
  data(){
      return{
        routes: "Home",
        debbieForm: false,
        debtor: [],
        debtData: null,
      }
  },
  methods: {
    switchRoute(route){
      this.routes = route
    },
    viewDebt(debtor){
      this.debtData = debtor;
      this.routes = "ViewDebt";
    },
    addNewDebtor(newdebtor){
      this.debtor.push(newdebtor);
    }
  }
}
</script>

<style> 
  html{
      overflow-y: hidden;
      padding: 0;
      margin: 0;
  }
  #container{
    display: flex;
    width: 100%;
    height: 100%;
    flex-direction: row;
  }
</style>