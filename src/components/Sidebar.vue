<template>
  <v-navigation-drawer permanent>
    <v-toolbar flat>
      <v-list>
        <v-list-tile>
          <v-list-tile-title class="title">
            Debby
          </v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-toolbar>
     <v-divider></v-divider>

    <v-list dense class="pt-0">
      <v-list-tile v-for="route in routes" @click="$emit('switchRoute', route)">
        <v-list-tile-action>
          <v-icon></v-icon>
        </v-list-tile-action>

        <v-list-tile-content>
          <v-list-tile-title>{{route}}</v-list-tile-title>
        </v-list-tile-content>
      </v-list-tile>
    </v-list>

   </v-navigation-drawer>


</template>

<script>
	export default{
		name: "Sidebar",
    data(){
      return{
        routes: ["Home", "Settings"]
      }
    }
	}
</script>

<style scoped>

</style>