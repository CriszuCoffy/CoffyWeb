<template>
  <header>
    <nav class="navbar">
      <div>
         <img :src="logo" @click="toggleBody('Main')" alt="Logo" />
      </div>
      <ul class="nav-links" @click="toggleMenu">
        <li v-for="tab in tabs" :key="tab.path" :class="['nav-item', { 'selected': this.bodyContent === tab.component.name }]" @click="toggleBody(tab.component.name)">
          <router-link :to="tab.path" class="nav-link" active-class="active">{{ tab.label }}</router-link>
        </li>
      </ul>
      <div class="hamburger" @click="toggleMenu">
        <span class="line"></span>
        <span class="line"></span>
        <span class="line"></span>
      </div>
    </nav>
  </header>
  <MainBody v-if="this.bodyContent==='Main'"/>
  <MainGames v-if="this.bodyContent==='MainGames'"/>
  <MainJams v-if="this.bodyContent==='MainJams'"/>
  <MainAboutUs v-if="this.bodyContent==='MainAboutUs'"/>
</template>

<script>

import MainBody from './components/mainbody.vue'
import MainGames from './components/games/gamesMain.vue'
import MainJams from './components/jams/jamsMain.vue'
import MainAboutUs from './components/knowUs/aboutUsMain.vue'
import logo from '@/assets/logo_sin_fondo_192x192.png';

export default {
  data() {
    return {
      // Definimos las pestañas del menú
      tabs: [
        { label: 'Games', component: MainGames },
        { label: 'Jams', component: MainJams },
        { label: 'About us', component: MainAboutUs },
        // { label: 'Portafolio', path: '/portfolio' },
        // { label: 'Contacto', path: '/contact' }
      ],
      isOpen: false, // Para manejar el estado del menú en dispositivos móviles
      bodyContent: 'Main',
      logo,
    }
  },
  name: 'App',
  components: {
    MainGames,
    MainBody,
    MainJams,
    MainAboutUs,
  },
  methods: {
    toggleMenu() {
      this.isOpen = !this.isOpen;
    },   
    toggleBody(component) {
      this.bodyContent = component
      console.log(this.bodyContent)
    },
  }
}
</script>

<style lang="scss" scoped>
/* Estilos del componente de cabecera */

.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.nav-item.selected {
  border-bottom: solid #010501; /* Estilo del borde para el elemento seleccionado */
  border-radius: 4px; /* Opcional: redondea las esquinas del borde */
}

img{
  width: 70px;
}

img:hover{
  width: 70px;
  background-color: #66689f;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-item {
  margin-left: 20px;
}

.nav-link {
  color: #fff;
  text-decoration: none;
  padding: 8px 15px;
  border-radius: 5px;
  transition: background-color 0.3s;
}

.nav-link:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.active {
  background-color: #388E3C; /* Color del enlace activo */
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.line {
  width: 25px;
  height: 3px;
  background-color: #fff;
  margin: 3px 0;
  transition: all 0.3s;
}

/* Estilos responsivos */
@media (max-width: 768px) {
  .nav-links {
    position: absolute;
    top: 60px;
    right: 0;
    background-color: #4CAF50;
    width: 100%;
    height: calc(100vh - 60px);
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transform: translateX(100%);
    transition: transform 0.5s;
    z-index: 1000;
  }

  .nav-item {
    margin: 15px 0;
  }

  .hamburger {
    display: flex;
  }

  .nav-links.active {
    transform: translateX(0);
  }
}
</style>
