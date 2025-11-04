<script setup>
  import { reactive, ref } from 'vue';

  const isMenuOpen = ref(false);

  const toggleMenu = () => {
    isMenuOpen.value = !isMenuOpen.value;
  };

  const closeMenu = () => {
    isMenuOpen.value = false;
  };


  const navItems = reactive([
    { name: 'INÍCIO', link: '#inicio' },
    { name: 'SERVIÇOS', link: '#servicos' },
    { name: 'CONTATO', link: '#contato' },
    { name: 'SOBRE NÓS', link: '#sobre-nos' },
    { name: 'NOSSOS PRODUTOS', link: '#products' },
  ]);
</script>

<template>
  <header class="navbar-wrapper">
    <nav class="navbar">
      <div class="navbar--logo">
        <img src="@/assets/LYMTT-LOGO.png" alt="LYMTT LOGO" class="logo-img" />
      </div>

      <button class="navbar--toggle" @click="toggleMenu" aria-label="Toggle navigation" :aria-expanded="isMenuOpen">
        <span class="bar"></span>
        <span class="bar"></span>
        <span class="bar"></span>
      </button>

      <div class="navbar--menu" :class="{ 'is-open': isMenuOpen }">
        <a v-for="item in navItems" :key="item.name" :href="item.link" class="navbar--link" @click="closeMenu">
          {{ item.name }}
        </a>
      </div>
    </nav>
  </header>
</template>

<style scoped lang="scss">
  @use "sass:color";
  $color-primary: #004c99;
  $color-text-menu: #337ab7;
  $color-bg-top: #222222;
  $color-bg-main: #ffffff;
  $breakpoint-mobile: 766px;

  .navbar-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1000;
    background-color: $color-bg-main;
    padding: 0 5%;


  }

  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    padding-right: 10%;
    background-color: $color-bg-main;

    &--logo {
      display: flex;
      align-items: center;

      .logo-img {
        height: 60px;
        width: auto;
      }
    }

    &--toggle {
      display: flex;
      flex-direction: column;
      justify-content: space-around;
      width: 30px;
      height: 25px;
      background: transparent;
      border: none;
      cursor: pointer;
      padding: 0;
      z-index: 100;

      .bar {
        width: 100%;
        height: 3px;
        background-color: $color-primary;
        transition: all 0.3s ease-in-out;
      }

      @media (min-width: $breakpoint-mobile) {
        display: none;
      }
    }

    &--menu {
      display: flex;
      gap: 30px;
      background-color: $color-bg-main;

      .navbar--link {
        color: $color-text-menu;
        font-weight: bold;
        text-decoration: none;
        transition: color 0.3s;
        font-size: 0.9em;

        &:hover {
          color: color.adjust($color-text-menu, $lightness: -15%)
        }
      }

      @media (max-width: $breakpoint-mobile) {

        position: absolute;
        top: 80px;
        left: 0;
        width: 100%;
        height: 100vh;
        flex-direction: column;
        align-items: center;
        padding: 20px 0;

        transform: translateX(100%);
        transition: transform 0.3s ease-in-out;
        overflow-y: auto;

        .navbar--link {
          font-size: 1.2em;
          width: 100%;
          text-align: center;
          padding: 15px 0;
          border-bottom: 1px solid color.adjust($color-primary, $lightness: 60%);
        }

        &.is-open {
          transform: translateX(0);
        }
      }

    }

    @media (min-width: $breakpoint-mobile) {
      &--menu {
        display: flex !important;
      }
    }
  }

  .navbar--toggle.is-open {
    .bar:nth-child(2) {
      opacity: 0;
    }

    .bar:nth-child(1) {
      transform: translateY(9px) rotate(45deg);
    }

    .bar:nth-child(3) {
      transform: translateY(-9px) rotate(-45deg);
    }
  }
</style>