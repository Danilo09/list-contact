<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <!-- <router-link to="/" class="navbar-brand">KZAS</router-link> -->
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <!-- <router-link to="/contacts" class="nav-link">Lista de contatos</router-link> -->
        </li>
        <li class="nav-item">
          <!-- <router-link to="/add" class="nav-link">Adicionar Novo</router-link> -->
        </li>
      </div>
    </nav>
    <FormContact/>
  </div>
</template>

<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/vue-material"></script>
<script>
import FormContact from './components/FormContact.vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'


export default {
  name: 'App',
  components: {
    FormContact
  }
}
</script>

<style>
#app {
  font-family: 'Quicksand', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
/*reset.css*/
/* RESETS */
*,
*::before,
*::after {
  box-sizing: border-box;
}
.row {
  margin: 0;
}
body {
  width: 100%;
  margin: 0 auto;
  color: #4d4d4d;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
}

button {
  height: 48px;
  color: rgb(255, 255, 255);
  font-size: 16px;
  font-weight: bold;
  line-height: 24px;
  text-align: center;
}
.btn-success {
  background: #f05e5c;
  border: 1px solid #f05e5c;
}
.btn-success:hover {
  background: #c25151;
  border: 1px solid #c25151;
}

.form-control {
  border: 1px solid #e7e7e7;
  border-radius: 4px;
  max-width: 472px;
  height: 40px;
}
.form-control:focus {
  border-color: #41a5bb;
  box-shadow: 0 0 0 0.2rem #41a5bb25
}

/*END RESETS*/
</style>
