<template>
  <div class="text-start">
    <div class="circle fs-2 float-end">
      <span class="text-uppercase" style="font-size: 40%">Punkte</span><br>
      {{ userInfo.points }}
      </div>
    <div class="fs-5 py-3">
      <b>Tere, {{ userInfo.username }}</b>
    </div>
    <div class="fs-6">
      Telefon: {{ userInfo.mobile }}
    </div>
  </div>

</template>
<script>
export default {
  name: 'UserName',
  data: function () {
    return {
      username: '',
      userInfo: {
        roleId: 0,
        username: '',
        points: 0,
        mobile: 0
      }
    }
  },
  methods: {
    getUserInfo: function () {
      this.$http.get("/users/me", {
            params: {
              userId: sessionStorage.getItem('userId')
            }
          }
      ).then(response => {
        this.userInfo = response.data
        this.$emit('emitUserInfoEvent', this.userInfo)
      }).catch(error => {
        console.log(error)
      })
    },
  },
  beforeMount() {
    this.getUserInfo()
  }
}
</script>