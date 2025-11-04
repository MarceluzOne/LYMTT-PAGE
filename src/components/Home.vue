<script setup>
</script>

<template>
  <section class="hero-section" id="inicio">
    <div class="hero-section__content">
      <h1 class="hero-section__title">
        Transformamos visões em realidade com soluções de
        software sob medida que aumentam a eficiência e
        estimulam a inovação
      </h1>
      <a href="#solicitar-orcamento" class="hero-section__button">
        Solicite seu orçamento
      </a>
    </div>
    <div class="hero-section__image">
      </div>
  </section>
</template>

<style scoped lang="scss">
$color-hero-bg: #004c99;
$color-hero-text: #ffffff;
$color-button-bg: #ffffff;
$color-button-text: #004c99;

.hero-section {
  background-color: $color-hero-bg;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 80px;
  padding: 5% 10% ;
  gap: 40px; 
  @media (min-width: 768px) {
    flex-direction: row;
    justify-content: center;
    padding: 80px 10%;
  }



  &__content {
    flex: 1;
    text-align: center;
    max-width: 600px;
    
    @media (min-width: 768px) {
      text-align: left;
      margin-right: 40px; 
    }
  }

  &__title {
    color: $color-hero-text;
    font-size: 2em;
    line-height: 1.3;
    text-align: center;
    margin-bottom: 30px;
    
    @media (min-width: 768px) {
      font-size:2em;
      text-align: justify;
    }
    @media (min-width: 1024px) {
      font-size: 2.5em; 
    }
  }

  &__button {
    display: inline-block;
    background-color: $color-button-bg;
    color: $color-button-text;
    padding: 15px 30px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: bold;
    font-size: 1.1em;
    transition: background-color 0.3s, color 0.3s;

    &:hover {
      background-color: lighten($color-button-text, 60%);
      color: $color-button-bg; 
    }
  }

  &__image {
    flex: 1;
    min-height: 400px; 
    width: 100%;
    background: url('../assets/hero-illustration.svg') no-repeat center center / contain;


    @media (max-width: 767px) {
        order: -1;
        min-height: 250px;
    }
    
    @media (min-width: 768px) {
        min-height: 400px;
    }

    @media (min-width: 1024px) {
        min-height: 500px;
    }
  }
}
</style>