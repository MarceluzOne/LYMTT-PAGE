<script setup>
import { reactive, ref } from 'vue';

const DESTINATION_EMAIL = 'lymtt.technology@gmail.com';

const formData = reactive({
  nome: '',
  assunto: '',
  mensagem: ''
});

const errors = reactive({
    nome: '',
    assunto: '',
    mensagem: ''
});

const isSubmitting = ref(false);

const validateForm = () => {
    let isValid = true;
    errors.nome = '';
    errors.assunto = '';
    errors.mensagem = '';

    if (formData.nome.trim().length < 3) {
        errors.nome = 'O nome deve ter pelo menos 3 caracteres.';
        isValid = false;
    }
    if (formData.assunto.trim().length === 0) {
        errors.assunto = 'O campo Assunto é obrigatório.';
        isValid = false;
    }
    if (formData.mensagem.trim().length < 10) {
        errors.mensagem = 'A mensagem é muito curta. Detalhe sua ideia (mínimo 10 caracteres).';
        isValid = false;
    }
    return isValid;
};


const submitForm = () => {

    if (!validateForm()) {
        return; 
    }

    isSubmitting.value = true;
    
    const subject = `[CONTATO] ${formData.assunto} (Por: ${formData.nome})`;
    const body = `Nome: ${formData.nome}\n\n${formData.mensagem}`;
    const mailtoUrl = `mailto:${DESTINATION_EMAIL}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
    setTimeout(() => {
        window.location.href = mailtoUrl;
        isSubmitting.value = false;
        formData.nome = '';
        formData.assunto = '';
        formData.mensagem = '';
    }, 500); 
};
</script>

<template>
  <section class="contact-section" id="contato">
    <div class="contact-section__header">
      <h2 class="contact-section__title">
        Transforme suas ideias em código
      </h2>
    </div>

    <div class="contact-section__container">
      
      <div class="contact-section__illustration">
        <img 
          src="@/assets/concept-message.svg" 
          alt="Pessoas trabalhando com email e código"
        />
      </div>

      <div class="contact-section__form-wrapper">
        <form @submit.prevent="submitForm" class="contact-form">
          
          <label class="form-label" for="nome">Nome</label>
          <input 
            id="nome"
            v-model="formData.nome"
            type="text" 
            class="form-input" 
            required
          />

          <label class="form-label" for="assunto">Assunto</label>
          <input 
            id="assunto"
            v-model="formData.assunto"
            type="text" 
            class="form-input" 
            required
          />

          <label class="form-label form-label--hint" for="mensagem">
            Envie sua ideia para que um de nossos especialistas entre em contato
          </label>
          <textarea 
            id="mensagem"
            v-model="formData.mensagem"
            class="form-textarea" 
            rows="5"
            required
          ></textarea>

          <div class="form-actions">
            <button type="submit" class="form-submit-button" :disabled="isSubmitting">
              {{ isSubmitting ? 'AGUARDE...' : 'ENVIAR' }}
            </button>
          </div>
        </form>
      </div>

    </div>
  </section>
</template>

<style scoped lang="scss">
$color-bg-blue: #004c99;
$color-text-light: #ffffff;
$color-card-bg: #ffffff;
$color-input-border: #cccccc;
$color-input-focus: #337ab7;

.contact-section {
  background-color: $color-bg-blue;
  padding: 80% 5%;
  @media (min-width: 420px){
    padding: 6% 5%;
  }
  @media (min-width: 520px){
    padding: 20% 5%;
  }
  @media (min-width: 770px){
    padding: 5% 5%;
  }
  
  
}

.contact-section__header {
  text-align: center;
  margin-bottom: 50px;
}

.contact-section__title {
  color: $color-text-light;
  font-size: 2em;
  font-weight: 600;
}

.contact-section__container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 40px;

  @media (min-width: 992px) {
    flex-direction: row;
    justify-content: center;
    align-items: flex-start;
  }
}

.contact-section__illustration {
  flex: 1;
  max-width: 450px;
  text-align: center;
  
  img {
    max-width: 100%;
    height: auto;
    display: block;
    margin: 0 auto;
  }
}

.contact-section__form-wrapper {
  flex: 1;
  max-width: 500px;
  background-color: $color-card-bg;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.contact-form {
  display: flex;
  flex-direction: column;
}

.form-label {
  font-size: 0.9em;
  font-weight: 500;
  color: #333;
  margin-top: 15px;
  margin-bottom: 5px;

  &--hint {
    font-size: 0.8em;
    font-style: italic;
    color: #666;
    margin-top: 0;
    margin-bottom: 5px;
  }
}

.form-input, .form-textarea {
  width: 100%;
  padding: 10px;
  border: 2px solid $color-input-border;
  border-radius: 5px;
  font-size: 1em;
  box-sizing: border-box;
  
  &:focus {
    outline: none;
    border-color: $color-input-focus;
    box-shadow: 0 0 0 2px rgba($color-input-focus, 0.3);
  }
}

.form-textarea {
  resize: vertical;
}

.form-actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 30px;
}

.form-submit-button {
  background-color: $color-input-focus;
  color: $color-text-light;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s;
  
  &:hover:not(:disabled) {
    background-color: darken($color-input-focus, 10%);
  }

  &:disabled {
    background-color: #999;
    cursor: not-allowed;
  }
}
</style>