<template>
  <div>
    <div>
      Test auth app
    </div>

    <div>
      <button v-on:click="sendAuthRequest">Auth</button>
    </div>

    <div>
      <button v-on:click="sendTestRequest">Test</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    sendTestRequest: function () {
      var c = this.getCookie(".AspNetCore.Identity.Application");
      let cookieValue = ".AspNetCore.Identity.Application=" + c;
      console.log(cookieValue);

      var myHeaders = new Headers();
      myHeaders.append("Cookie", cookieValue);

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch("https://localhost:44377/api/v1/Test/Foo", requestOptions)
        .then(response => response.text())
        .then(result => console.log(result))
        .catch(error => console.log('error', error));
    },

    sendAuthRequest: function () {
      var myHeaders = new Headers();
      myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

      var urlencoded = new URLSearchParams();
      urlencoded.append("Email", "student_025@a-techs.io");
      urlencoded.append("Password", "111111");
      urlencoded.append("RememberMe", "true");

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: urlencoded,
        redirect: 'follow'
      };

      fetch("https://localhost:44377/Public/Account/Login", requestOptions)
        .then(response => {
          console.log(response);
          return response.text()
        })
        .then(result => console.log(result))
        .catch(error => console.log('error', error));

      // this.setCookie('.AspNetCore.Identity.Application', 'CfDJ8LMlWLvwpy1Fh3Ygy9iTBkxW2GRNijZLQ3CeSPlEZi2rhXWwZ-VTzxEBCxwLKNrA6Gma7RF8cdzdde01Is_l73sArQYcg9mgumCK_mJkXodTeEbZp9yjXICmdORaFN6OjGrpL0N2LttTHmCKAuLE9GQEhvfai-qUkT-utWLa6njZDkkudUcJ4ixR31HOaeLApaR2b9_fEt9Ty5zTisdQo7PhrUA7mtS0f3pdYrioh6P3wv4TkN-Z5XlGHYzsVc99dIa7uvo0aNibQS0oz-LHOkfo1zKhc44ceAg6T6v8E0erXmDBaM8CCi4uOsd1SgBmz-b3ntl3SRCh70EFlNeOPZqJqFgbgnkuT3YMxp940uBuiR4XoHRP6NZIuXxnfcOZi_uB_2E_KnTkYueyQsmjR0KO3XaFcvlDn8MsRzRXT71qLGF1d2zYXhHr_uGalcTAQGJ-n5VEegp1hbICvIq7Forg8BdWPnI3juu0CSrjfPOE7TAwQZlSOmVmNmlVApoi0LnLqe1umcbKCT576LXkSw8LXs5-cemB-KQJ-mRoOszlOiFYzYKF01hR6ErKrD-BT33l08xDGcFpX4S69tA2vQ0AsKMnMPwidza7-jmtWyk2OUqNictwrn9o5E9YiLWgVWxJ8Vov6rR4wHnP51ZCPwu_FtZQ42msOx4YSHC6yDpv9KRg-R4NkGdgGZ9XxTnqo1YRNqSorxsUgo4d-3HVs07Y6d4anqMrLl8myvsg6mwzT9q8bo9UayqTaOjGJzUnr9iseH_Tc6xKuStJKqTDKgz0NFbYIsj54hypfdhyc60ui3MIrnMJ3JujHt6Phdv6CD-Q_HpyOJgESupsx9WBoTRLevSiS9IpIekXV1sec-0mzCKnn3nY1dxjDONNHrLXZuqAeavr27nDILKZFM7Cn1I0vtsKUcKNgZPt9y_1VPjBIjppTPS3IT0QRe7NHskr4myU3oOn_uMP5Ci8zAXPUhUfTlt12AxpyWJslQJEH3dH13lm6rkOmMay1JAl4rkqOHMGYCZgH67hCJ1HcvwtVuJbuB9S_gwnPG0IbxJhnya2gI_Q6aXPVSVSuZT0mu1Zsl6iwKTHYpYuN3BlbrpbHrA', { secure: true, 'max-age': 3600 });
    },

    getCookie: function (name) {
      const value = `; ${document.cookie}`;
      const parts = value.split(`; ${name}=`);
      if (parts.length === 2) return parts.pop().split(';').shift();
    },

    setCookie: function (cname, cvalue, exdays) {
      var d = new Date();
      d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
      var expires = "expires=" + d.toUTCString();
      document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
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
