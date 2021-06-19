<template>
  <form @submit.prevent="confirmEditProfile">
    <div class="card-body p-5">
      <img :src="user.avatarUrl" style="width: 20%; margin-left: 40%;">


      <div class="row">
        <div class="col-md-12 col-lg-6 col-sm-12">

          <label class="mt-2">Nom</label>
          <input class="form-control" type="text" v-model="user.lastName">

          <label class="mt-2">Prénom</label>
          <input class="form-control" type="text" v-model="user.firstName">

          <label class="mt-2">Date de naissance</label>
          <input class="form-control" type="date" v-model="user.birthDate">

          <label class="mt-2">Téléphone</label>
          <input class="form-control" type="tel" v-model="user.phone">

        </div>

        <div class="col-md-12 col-lg-6 col-sm-12">

          <label class="mt-2">Genre</label>
          <input class="form-control" type="text" v-model="user.gender">

          <label class="mt-2">E-mail</label>
          <input class="form-control" type="text" v-model="user.email">

          <label class="mt-2">Détails</label>
          <textarea class="form-control"  v-model="user.details"/>


          <label class="mt-2">URL de l'image de profil</label>
          <input class="form-control" type="text" v-model="user.avatarUrl">

        </div>
      </div>
      <button type="submit" class="btn btn-primary">
        Enregistrer les modifications
      </button>

      <button id="close" type="button" @click="closeForm" class="btn btn-danger">
        Annuler
      </button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'Form',
  props: [ "initialValues" , "addClasses"],
  data() {
    return {
      user: this.initialValues,
    }
  },

  methods: {
    confirmEditProfile() {
      this.$emit("submit", this.user)
    },
    closeForm() {
      this.$emit("cancel")
    }
  }
}
</script>

<style>
.mt-2 {
  font-size: 19px;
  color: #34495E;
  font-weight: 700;
}
.btn-primary {
  margin-left: 35%;
}
.btn {
  margin-top: 5%;
}
</style>
