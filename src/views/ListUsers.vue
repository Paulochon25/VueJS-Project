<template>
  <div class="container-fluid">
    <Header v-on:fetch-user="fetchUsers" @mask="showMaskMethod"/>

    <Table :users="users"/>
  </div>
</template>

<script>
import Header from "../components/Header";
import Table from "../components/Table";

export default {
  data() {
    return {
      users: [],
    };
  },
  components: { Header, Table },
  methods: {
    fetchUsers(users) {
      this.users = users;
    },

    showMaskMethod(mask) {
      this.$emit('mask', mask)
    }
  },
};
</script>
<style>
body {
  background-color:#c1b6b6;
}
div.card.mb-2 {
  background-color: #34495E;
  border: 2px solid #34495E;
}
div.col-md-4 {
  color: #c1b6b6;
}
#tbl-users{
  background-color: #34495E;
  color: #c1b6b6;
  border-radius: 20px;
}
thead {
  border-top: 0;
}
thead:hover {
  color: #5DADE2;
}
tr:hover {
  color: #95A5A6;
}
.card-body {
  background-color: #6c757d;
  border: 2px solid #6c757d;
}
</style>
