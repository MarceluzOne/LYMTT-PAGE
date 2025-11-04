<script setup>
  import { reactive } from 'vue';

  const product = reactive({
    name: 'WeDo',
    tagline: 'Transforme Metas em Hábitos Duradouros.',
    headline: 'O Aplicativo Web para Criar e Acompanhar Seus Hábitos Saudáveis',
    description: [
      'O WeDo é uma solução de gerenciamento de metas e tarefas focada em engajamento. Com uma interface intuitiva e design mobile-first (como um app nativo), tornamos a criação de hábitos saudáveis (como exercícios, leitura ou estudo) uma experiência divertida e recompensadora.',
      'Construído para rodar no seu navegador (desktop e mobile), o WeDo não exige instalação, oferecendo a mesma experiência fluida de um aplicativo, garantindo que suas metas estejam sempre ao seu alcance.'
    ],
    cta: 'Solicitar Acesso à Demonstração',
    features: [
      'Busca e Criação de Desafios Personalizados',
      'Acompanhamento de Progresso Visual (em %)',
      'Interface Mobile-First Amigável',
      'Gamificação para Engajamento'
    ]
  });
</script>

<template>
  <section class="wedo-section" id="produtos">
    <div class="wedo-container">

      <h2 class="section-title">{{ product.headline }}</h2>

      <div class="product-highlight-block">

        <div class="product-highlight__image-mockup">
          <img src="@/assets/wedo-app-mobile.png" alt="Interface mobile do aplicativo WeDo com lista de desafios"
            class="app-screenshot" />
        </div>

        <div class="product-highlight__content">
          <p class="product-tagline">{{ product.tagline }}</p>

          <div class="product-description">
            <p v-for="(p, index) in product.description" :key="index">{{ p }}</p>
          </div>

          <div class="product-features">
            <h4>Foco em Resultados:</h4>
            <ul>
              <li v-for="(feature, index) in product.features" :key="index">
                <span class="check-icon">&#10003;</span> {{ feature }}
              </li>
            </ul>
          </div>

          <a href="#contato" class="cta-button">
            {{ product.cta }}
          </a>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
  @use "sass:color";

  $color-bg-light: #f4f4f4;
  $color-primary: #004c99;
  $color-text-dark: #333333;
  $color-highlight: #337ab7;

  .wedo-section {
    background-color: $color-bg-light;
    padding-inline: 5%;
    color: $color-text-dark;

  }

  .wedo-container {
    max-width: 1100px;
    margin: 0 auto;
    text-align: center;
  }

  .section-title {
    font-size: 2.2em;
    font-weight: 700;
    color: $color-primary;
    margin-bottom: 50px;
  }

  .product-highlight-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 60px;

    @media (min-width: 992px) {
      flex-direction: row;
      text-align: left;
      gap: 80px;
    }
  }

  .product-highlight__image-mockup {
    flex-shrink: 0;
    max-width: 350px;
    @media (min-width: 992px) {
      order: -1;
      max-width: 380px;
    }

    .app-screenshot {
      width: 100%;
      height: auto;
      border-radius: 20px;
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
    }
  }

  .product-highlight__content {
    flex: 1;
    max-width: 600px;

    @media (max-width: 991px) {
      text-align: center;
    }
  }

  .product-tagline {
    font-size: 1.5em;
    font-weight: 600;
    color: $color-highlight;
    margin-bottom: 20px;
  }

  .product-description p {
    line-height: 1.6;
    margin-bottom: 15px;
    font-size: 1em;
    text-align: justify;
  }

  .product-features {
    margin-top: 30px;

    h4 {
      font-size: 1.1em;
      color: $color-primary;
      margin-bottom: 10px;
    }

    ul {
      list-style: none;
      padding: 0;

      @media (min-width: 500px) {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
      }
    }

    li {
      line-height: 1.8;
      font-size: 1em;
      text-align: left;

      .check-icon {
        color: $color-highlight;
        font-weight: bold;
        margin-right: 5px;
      }
    }
  }

  .cta-button {
    display: inline-block;
    background-color: $color-primary;
    color: white;
    padding: 15px 30px;
    border-radius: 6px;
    text-decoration: none;
    font-weight: bold;
    margin-top: 40px;
    transition: background-color 0.3s;

    &:hover {
      background-color: color.adjust($color-primary, $lightness: -10%)
    }
  }
</style>