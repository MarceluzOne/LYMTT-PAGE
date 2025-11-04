<script setup>
  import { reactive } from 'vue';
  const getIconPath = (iconName) => {
    try {
      const filename = iconName.split('/').pop();
      return new URL(`../assets/${filename}`, import.meta.url).href;
    } catch (error) {
      console.error("Erro ao resolver caminho do ícone:", iconName, error);
      return null;
    }
  };

  const rawServices = [
    {
      path: 'code.svg',
      title: 'Aplicações de Alta Performance',
      description:
        'A velocidade é a primeira impressão do seu negócio online. Desenvolvemos aplicações ultra-rápidas e otimizadas que cativam o usuário, melhoram seu ranking no Google e transformam visitantes em clientes.'
    },
    {
      path: 'server.svg',
      title: 'Back-end Robusto e Escalável',
      description:
        'Sua aplicação precisa estar pronta para o seu sucesso. Construímos a base do seu sistema com tecnologias seguras e eficientes garantindo estabilidade para suportar picos de tráfego e o crescimento do seu negócio.'
    },
    {
      path: 'game-icons_progression.svg',
      title: 'Modernização de Aplicações',
      description:
        'Seu sistema legado está limitando seu potencial? Modernizamos e literalizamos com tecnologia de ponta, melhorando a eficiência, a segurança e a experiência do usuário para levar sua operação para o próximo nível.'
    },
    {
      path: 'majesticons_ux-circle-line.svg',
      title: 'UX Focado em Conversão',
      description:
        'Um design não deve ser apenas bonito, ele precisa ser inteligente. Criamos interfaces intuitivas e um protocolo de usuário fluído que conduzem seus clientes de forma natural até a compra, eliminando barreiras e aumentando a satisfação.'
    },
    {
      path: 'mdi_shield-check.svg',
      title: 'Segurança Digital',
      description:
        'Proteja seus dados e a confiança de seus clientes. Implementamos as mais rigorosas práticas de segurança em cada camada da aplicação, criando uma fortaleza digital para o seu negócio operar com tranquilidade.'
    }
  ];

  const services = reactive(
    rawServices.map((service) => ({
      ...service,
      icon: getIconPath(service.path)
    }))
  );
</script>

<template>
  <section class="services-wrapper" id="servicos">
    <div class="services-wrapper__container">
      <h2 class="services-title">
        NOSSOS SERVIÇOS
      </h2>

      <div class="services-grid">
        <div v-for="(service, index) in services" :key="index" class="service-card">
          <div class="service-card__box">
            <div class="service-card__icon">
              <img :src="service.icon" :alt="service.title + ' Icon'" class="icon-svg" />
            </div>

            <div class="service-card__text-content">
              <h3 class="service-card__title">{{ service.title }}</h3>
              <p class="service-card__description">{{ service.description }}</p>
            </div>
          </div>
        </div>
        <div class="cta-block">
          <div class="cta-block__content">
            <p class="cta-block__text">
              Vamos conversar sobre como nossas soluções podem ajudar a impulsionar seus resultados. Entre em contato e
              transforme seu projeto em realidade.
            </p>
            <a href="#fale-conosco" class="cta-block__button">
              Fale com um especialista
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
  @use "sass:color";

  $color-bg-blue: #004c99;
  $color-text-light: #ffffff;
  $color-card-border: #337ab7;
  $color-card-bg: #ffffff;
  $color-cta-button: #ffffff;
  $color-cta-text: #004c99;

  .services-wrapper {
    background-color: $color-bg-blue;
    padding-inline: 10%;
    padding-bottom: 40%;
    color: $color-text-light;
    height: auto;

    @media(min-width: 1000px) {
      padding-bottom: 10%;
    }
  }

  .services-title {
    text-align: center;
    padding-top: 5%;
    font-size: 2em;
    font-weight: 700;
    margin-bottom: 50px;
    letter-spacing: 1px;
  }

  .services-grid {
    display: grid;
    grid-template-columns: 1fr;
    align-items: stretch;
    gap: 4%;

    @media (min-width: 600px) {
      gap: 6%;
    }

    @media (min-width: 992px) {
      gap: 8%;
      grid-template-columns: repeat(2, 1fr);

    }
  }

  .service-card {
    &__box {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
      height: 80%;
      padding: 30px;
      background-color: white;
      color: #004C99;
      border-radius: 8px;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s;

      @media (min-width: 520px) {
        flex-direction: row;
      }
    }

    &__icon {
      font-size: 3em;
      background-color: white;
      margin-bottom: 15px;
      padding: 10px;
      font-weight: 300;
      width: 60px;
      height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;

      @media(min-width: 520px) {
        padding: 30px;
      }

      span {
        display: block;
      }
    }

    &__title {
      font-size: 1.3em;
      font-weight: 600;
      margin-bottom: 10px;
      background-color: white;
      color: #004C99
    }
  }


  .cta-block {

    &__content {
      color: $color-text-light;
      padding: 10px;
      display: flex;
      flex-direction: column;
      justify-content: right;
      align-items: center;
      @media(min-width: 530px){
        align-items: end;
      }
    }

    &__text {
      font-size: 1.5em;
      line-height: 1.4;
      margin-bottom: 20px;
      text-align: center;
      @media(min-width: 500px){
        text-align: justify;
      }


      strong {
        font-weight: 700;
      }
    }

    &__button {
      padding: 12px;
      color: white;
      padding: auto;
      text-align: center;
      right: 0px;
      width: 200px;
      border: white 3px solid;
      text-decoration: none;
      font-weight: bold;
      border-radius: 5px;
      transition: background-color 0.3s;
      font-size: 1em;

      &:hover {
        background-color: color.adjust($color-cta-button, $lightness: -10%)
      }
    }
  }
</style>