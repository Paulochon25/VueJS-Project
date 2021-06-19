<template>
  <div class="container mt-5">
    <div v-if="!showModal">
      <div id="edit-informations-block">
        <p class="edit-user-field">Photo de profil</p>
        <img :src="user.avatarUrl" style="width: 20%">

        <div>

          <p class="edit-user-field">Nom</p>
          <p>
            {{ user.firstName }}
          </p>
          <p class="edit-user-field">E-mail</p>
          <p>
            {{ user.email }}
          </p>
          <p class="edit-user-field">Prénom</p>
          <p>
            {{ user.lastName }}
          </p>
          <p class="edit-user-field">Genre</p>
          <p>
            {{ user.gender }}
          </p>
          <p class="edit-user-field">Détails</p>

          <p v-html="showInformations"></p>
        </div>


        <button @click="showModal = true" class="btn btn-danger">
          Editer les informations
        </button>

      </div>
    </div>

    <Form v-else :initial-values="user" @submit="updateUserInformations" @cancel="closeModal"/>
  </div>
</template>
<script>
import axios from "axios";
import Form from "@/components/Form";

export default {
  name: 'Details',
  components: { Form },
  data() {
    return {
      user: {
        avatarUrl: "https://sumaleeboxinggym.com/wp-content/uploads/2018/06/Generic-Profile-1600x1600.png"
      },
      showModal: false
    }
  },
  computed: {
    showInformations() {
      return this.user.details;
    }
  },
  methods: {
    async getUserInformations() {
      const { data: user } = await axios(`https://ynov-front.herokuapp.com/api/users/${ this.$route.params.id }`)
      this.user = {
        ...user.data
      }
    },

    async updateUserInformations(currentUser) {
      try {
        await axios.put(`https://ynov-front.herokuapp.com/api/users/${ this.$route.params.id }`, currentUser)

      } catch(e) {
        console.log('Erreur dans la modification de l\'utilisateur : ' + e)
      }


    },

    closeModal() {
      this.showModal = false
    }
  },
  created() {
    this.getUserInformations()
  }
}
</script>
<style>
.edit-user-field {
  font-size: 20px;
  color: red;
  border-bottom: 1px solid red;
}
#edit-informations-block {
  background-color: #34495E;
  color: white;
  text-align: center;
  width: 50%;
  height: 57%;
  margin-left: auto; margin-right: auto;
  padding: 2%;
}
</style>