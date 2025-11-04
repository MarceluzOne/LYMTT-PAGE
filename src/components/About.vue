<script setup>
  import { reactive } from 'vue';


  const getPhotoPath = (photoFileName) => {
    try {
      return new URL(`../assets/us/${photoFileName}`, import.meta.url).href;
    } catch (error) {
      console.error("Erro ao resolver caminho da foto:", photoFileName, error);
      return null;
    }
  };

  const teamMembersData = [
    {
      name: 'Laryssa oliveira',
      role: 'Arquiteto Backend',
      description: 'Especialista em desenvolvimento e arquitetura back-end.',
      github: 'https://github.com/2002Larissa',
      photo: 'larissa.jpg'
    },
    {
      name: 'Yasmim Camille',
      role: 'Especialista em Qualidade (QA)',
      description: 'Especialista em garantia da qualidade de software, com foco na validação de arquitetura e desenvolvimento front-end.',
      github: 'https://github.com/YasmimB-Lira',
      photo: 'yasmim.jpg'
    },
    {
      name: 'Marcelo Arruda',
      role: 'Desenvolvedor Frontend',
      description: 'Combina os frameworks frontend para entrega escalavel.',
      github: 'https://github.com/MarceluzOne',
      photo: 'marcelo.jpg'
    },
    {
      name: 'Thialy Lima',
      role: 'Desenvolvedora Full-stack',
      description: 'Especialista em desenvolvimento full-stack, com foco em performance e escalabilidade de aplicações.',
      github: 'https://github.com/thialylima',
      photo: 'thialy.jpg'
    },
    {
      name: 'Thailan Sousa',
      role: 'Egenheiro de Software',
      description: 'Especialista dedicado ao desenvolvimento e à segurança da informação.',
      github: 'https://github.com/ThailanSousa',
      photo: 'thailan.jpg'
    }
  ];

  const teamMembers = reactive(
    teamMembersData.map((member) => ({
      ...member,
      photoPath: getPhotoPath(member.photo)
    }))
  );
</script>

<template>
  <section class="about-us-section" id="sobre-nos">
    <div class="about-us-container">

      <h2 class="section-title">Nossa História e Missão</h2>

      <div class="mission-block">
        <p class="mission-text">
          Nascemos da paixão por transformar processos complexos em soluções digitais elegantes e eficientes. Nossa
          missão é ser o parceiro tecnológico que impulsiona a inovação, garantindo que nossos clientes, operem com o
          máximo de performance e segurança.
        </p>
        <p class="mission-text">
          Acreditamos em código limpo, em metodologias ágeis e, acima de tudo, no poder da colaboração. Somos uma equipe
          enxuta, mas extremamente especializada, pronta para levar a sua visão do papel para o código.
        </p>
      </div>

      <h2 class="section-title team-title">Conheça a Equipe</h2>

      <div class="team-grid">
        <div v-for="member in teamMembers" :key="member.name" class="member-card">
          <div class="member-card__photo-wrapper">
            <img :src="member.photoPath" :alt="member.name" class="member-card__photo" />
          </div>
          <div>
            <h3 class="member-card__name">{{ member.name }}</h3>
            <p class="member-card__role">{{ member.role }}</p>
            <p class="member-card__description">{{ member.description }}</p>
          </div>
          <div>
            <a style="color:black" :href="member.github" target="_blank">
              <font-awesome-icon :icon="['fab', 'github']" />
            </a>
          </div>

        </div>
      </div>
      <div class="team-grid">

      </div>

    </div>
  </section>
</template>

<style scoped lang="scss">
  $color-bg-light: #f4f4f4;
  $color-primary: #004c99;
  $color-text-dark: #333333;
  $color-text-highlight: #337ab7;

  .about-us-section {
    background-color: $color-bg-light;
    padding: 80px 5%;
    color: $color-text-dark;
  }

  .about-us-container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .section-title {
    text-align: center;
    font-size: 2em;
    font-weight: 700;
    color: $color-primary;
    margin-bottom: 40px;
  }

  .mission-block {
    max-width: 800px;
    margin: 0 auto 60px;
    text-align: center;

    .mission-text {
      font-size: 1.1em;
      line-height: 1.6;
      margin-bottom: 20px;
    }
  }

  .team-title {
    margin-top: 40px;
    margin-bottom: 40px;
  }

  .team-grid {
    display: grid;
    gap: 30px;
    padding-bottom: 40px;

    grid-template-columns: 1fr;

    @media (min-width: 600px) {
      grid-template-columns: repeat(2, 1fr);
    }

    @media (min-width: 1024px) {
      grid-template-columns: repeat(5, 1fr);
    }
  }

  .member-card {
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    padding: 20px;
    border-radius: 8px;
    background-color: $color-bg-light;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);

    &__photo-wrapper {
      width: 120px;
      height: 120px;
      margin: 0 auto 15px;
      border-radius: 50%;
      overflow: hidden;
      border: 3px solid $color-text-highlight;
    }

    &__photo {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    &__name {
      font-size: 1.4em;
      font-weight: 700;
      color: $color-primary;
      margin-bottom: 5px;
    }

    &__role {
      font-size: 0.9em;
      font-weight: 600;
      color: $color-text-highlight;
      margin-bottom: 10px;
    }

    &__description {
      font-size: 0.9em;
      color: #666;
    }
  }
</style>