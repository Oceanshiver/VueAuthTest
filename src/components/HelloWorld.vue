<template>
  <div>
    <div>
      Test auth app
    </div>

    <div>
      <button v-on:click="getUserGroups">Test</button>
    </div>
  </div>
</template>

<script>

const AUTH_SECRET_KEY = "12345";
const AUTH_USER_UID = "cf88adc3-f749-4cf9-8914-b660f3b5b8e1";

export default {
  props: {
    msg: String
  },
  methods: {
    getUserGroups: function () {
      var authStr = btoa(AUTH_SECRET_KEY + "|" + AUTH_USER_UID);
      var myHeaders = new Headers();
      myHeaders.append("HubCloudCustomAuth", authStr);

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch("https://localhost:44377/api/v1/UserGroup/GetUserGroupList", requestOptions)
        .then(response => response.text())
        .then(result => console.log(result))
        .catch(error => console.log('error', error));
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
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
</style>
