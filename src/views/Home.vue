<template>
  <v-jumbotron
    :gradient="gradient"
    dark
    src="https://cdn.pixabay.com/photo/2018/07/25/16/00/decorated-3561710__480.jpg"
  >
    <v-container fill-height>
      <v-layout align-center>
        <v-flex text-xs-center>
          <h3 class="display-3">Welcome to the Site</h3>
          <span class="subheading">The simple app let you manage your employees.</span>
        </v-flex>
      </v-layout>
    </v-container>
  </v-jumbotron>
</template>

<script>
  export default {
    data: () => ({
       gradient: 'to top right, rgba(71,102,121, .7), rgba(25,32,72, .7)'
    })
  }
</script>