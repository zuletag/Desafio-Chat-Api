<template>
  <div class="container mt-5">
    <div class="row align-items-center">
      <!-- Usuario A -->
      <div class="col-3 text-center d-block">
        <img :src="usuarioA?.picture.large" alt="User A" class="img-fluid mb-2">
        <h5>{{ usuarioA?.name.first }} {{ usuarioA?.name.last }}</h5>
        <!-- Input para Person A -->
        <input type="color" class="form-control-color mb-2 w-100" v-model="colorA">
        <textarea class="form-control mb-2 " v-model="nuevoMensajeA" rows="5" placeholder="Escribe un mensaje..."></textarea>
        <button class="btn btn-primary" @click="sendMessage('A')">Enviar como {{ usuarioA?.name.first }}</button>
      </div>

      <!-- Chat -->
      <div class="col-6">
        <Chat :messages="mensajes" :userA="usuarioA" :userB="usuarioB" />
      </div>

      <!-- Usuario B -->
      <div class="col-3 text-center d-block">
        <img :src="usuarioB?.picture.large" alt="User B" class="img-fluid mb-2">
        <h5>{{ usuarioB?.name.first }} {{ usuarioB?.name.last }}</h5>
        <!-- Input para Person B -->
        <input type="color" class="form-control-color mb-2 w-100" v-model="colorB">
        <textarea class="form-control mb-2" v-model="nuevoMensajeB" rows="5" placeholder="Escribe un mensaje..."></textarea>
        <button class="btn btn-primary" @click="sendMessage('B')">Enviar como {{ usuarioB?.name.first }}</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Chat from './components/Chat.vue';

export default {
  components: {
    Chat,
  },
  data() {
    return {
      usuarios: [],
      mensajes: [],
      nuevoMensajeA: '',
      nuevoMensajeB: '',
      colorA: '#dc3545',
      colorB: '#0d6efd',
    };
  },
  async mounted() {
    await this.cargarUsuarios();
  },
  computed: {
    usuarioA() {
      return this.usuarios[0];
    },
    usuarioB() {
      return this.usuarios[1];
    }
  },
  methods: {
    async cargarUsuarios() {
      const url = 'https://randomuser.me/api/?results=2';
      const { data } = await axios.get(url);
      this.usuarios = data.results;
    },
    sendMessage(user) {
      let message;
      if (user === 'A' && this.nuevoMensajeA.trim()) {
        message = {
          sender: 'Person A',
          text: this.nuevoMensajeA,
          color: this.colorA,
        };
        this.nuevoMensajeA = '';
      } else if (user === 'B' && this.nuevoMensajeB.trim()) {
        message = {
          sender: 'Person B',
          text: this.nuevoMensajeB,
          color: this.colorB,
        };
        this.nuevoMensajeB = '';
      }

      if (message) {
        this.mensajes.push(message);
      }
    }
  }
};
</script>

<style>

</style>

