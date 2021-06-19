<template>
  <div @close="closeModal" class="modal" id="myModal" style="display: block;">
    <div class="modal-dialog modal-xl shadow-lg modal-dialog-scrollable">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h4 class="modal-title">Créer un utilisateur</h4>
          <button type="button" class="close" @click="closeModal" data-dismiss="modal">×</button>
        </div>
        <!-- Modal body -->
        <div class="modal-body">
          <add-user-form :initial-values="user" @submit="createUser"/>
        </div>
        <!-- Modal footer -->
        <div class="modal-footer">
          <button type="button" @click="closeModal" class="btn btn-danger" data-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import addUserForm from '../components/addUserForm.vue'

export default {
  name: "Modal",
  components: { addUserForm },
  data() {
    return {
      showModal: false,
      user: {
        avatarUrl: 'https://robohash.org/bf98349402674766c719ecc9ac50a48f?set=set4&bgset=&size=400x400'
      }
    };
  },
  methods: {
    closeModal() {
      this.$emit('closemodal')
    },

    async createUser(userCreated) {
      try {
        await axios.post(`https://ynov-front.herokuapp.com/api/users`, userCreated)

        this.$emit('closemodal')

        this.fetchUsers(userCreated)
      } catch (e) {
        console.log('Erreur dans la création de l\'utilisateur : ' + e);
      }
    }
  }
};
</script>


<style lang="scss" scoped>
.modal {
  overflow-x: hidden;
  overflow-y: auto;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 9;

  &__backdrop {
    background-color: rgba(0, 0, 0, 0.3);
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1;
  }

  &__dialog {
    background-color: #ffffff;
    position: relative;
    width: 600px;
    margin: 50px auto;
    display: flex;
    flex-direction: column;
    border-radius: 5px;
    z-index: 2;
    @media screen and (max-width: 992px) {
      width: 90%;
    }
  }

  &__close {
    width: 30px;
    height: 30px;
  }

  &__header {
    padding: 20px 20px 10px;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
  }

  &__body {
    padding: 10px 20px 10px;
    overflow: auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  &__footer {
    padding: 10px 20px 20px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
div.modal-footer, div.modal-header {
  background-color: #34495E;
  color: white;
}
div.modal-body {
  padding-top: 2%;
}
button.close {
  font-size: 32px;
  font-weight: 700;
  color: white;
}
.modal-title {
  font-weight: 300;
  margin-left: 1%;
}
</style>
