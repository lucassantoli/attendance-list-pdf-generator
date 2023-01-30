<template>
  <div class="home container">
    <div class="title-container">
      <span class="page-title">
        Monte<br/>sua lista de<br/>presença<br/>para casais<span class="colorful-animation">.</span>
      </span>
    </div>

    <div class="details">
      <p>Informe título do evento, o nome de cada conjuge participante e os dias em que o evento ocorrerá.</p>
      <p>Após isso, é só clicar em "Gerar lista" e o arquivo PDF será baixado automaticamente</p>
    </div>

    <Separator>Vamos começar!</Separator>

    <!-- Form -->

    <div class="step">
      <StepIndicator class="pink">1</StepIndicator>
      <div class="step-title">Título do evento</div>
      <Input v-model="title"/>
    </div>
    
    <div class="step">
      <StepIndicator class="orange">2</StepIndicator>
      <div class="step-title">Casais participantes</div>
      
      <div
        class="couple-detail"
        v-for="(couple, index) in participants"
        :key="index"
      >
        <div class="names">
          <span v-text="couple.male"></span>
          <span v-text="couple.female"></span>
        </div>
        <div class="action" @click="removeCouple(index)">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19,4H15.5L14.5,3H9.5L8.5,4H5V6H19M6,19A2,2 0 0,0 8,21H16A2,2 0 0,0 18,19V7H6V19Z" /></svg>
        </div>
      </div>

      <div class="couple-input">
        <div class="icon-input">
          <div class="icon"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M9,9C10.29,9 11.5,9.41 12.47,10.11L17.58,5H13V3H21V11H19V6.41L13.89,11.5C14.59,12.5 15,13.7 15,15A6,6 0 0,1 9,21A6,6 0 0,1 3,15A6,6 0 0,1 9,9M9,11A4,4 0 0,0 5,15A4,4 0 0,0 9,19A4,4 0 0,0 13,15A4,4 0 0,0 9,11Z" /></svg></div>
          <Input v-model="couple.male"/>
        </div>
        <div class="icon-input">
          <div class="icon"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M12,4A6,6 0 0,1 18,10C18,12.97 15.84,15.44 13,15.92V18H15V20H13V22H11V20H9V18H11V15.92C8.16,15.44 6,12.97 6,10A6,6 0 0,1 12,4M12,6A4,4 0 0,0 8,10A4,4 0 0,0 12,14A4,4 0 0,0 16,10A4,4 0 0,0 12,6Z" /></svg></div>
          <Input v-model="couple.female"/>
        </div>
      </div>

      <Button
        @click="addCouple"
        dark
        class="orange"
      >Adicionar casal</Button>
    </div>
    
    <div class="step">
      <StepIndicator class="cyan">3</StepIndicator>
      <div class="step-title">Dias de evento</div>
      
      <div
        class="day-detail"
        v-for="(day, index) in days"
        :key="index"
      >
        <div class="names">
          <span v-text="day"></span>
        </div>
        <div class="action" @click="removeDay(index)">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path d="M19,4H15.5L14.5,3H9.5L8.5,4H5V6H19M6,19A2,2 0 0,0 8,21H16A2,2 0 0,0 18,19V7H6V19Z" /></svg>
        </div>
      </div>

      <Input
        class="day-input"
        v-model="inputDay"
        placeholder="DD/MM"
      />

      <Button
        @click="addDay"
        dark
        class="cyan"
      >Adicionar dia</Button>
    </div>

    <!-- -->

    <Separator>Tudo pronto</Separator>

    <Button
      class="generate-attendance-list"
      @click="addDay"
    >Gerar lista</Button>

    <sdg />
  </div>
</template>

<script>
export default {
  name: 'Home',

  data: () => ({
    title: "",
    participants: [],
    days: [],
    couple: {
      male: "",
      female: ""
    },
    inputDay: "",
  }),

  methods: {
    addCouple: function() {
      this.participants.push({
        male: this.couple.male,
        female: this.couple.female,
      })

      this.couple = { male: "", female: "" };
    },

    removeCouple: function(index) {
      this.participants.splice(index, 1)
    },
    
    addDay: function() {
      this.days.push( this.inputDay )

      this.inputDay = "";
    },

    removeDay: function(index) {
      this.days.splice(index, 1)
    },
  }
}
</script>

<style lang="scss">
@import "@/styles/variables.scss";

.home {
  display: flex;
  flex-direction: column;
  
  .title-container {
    padding-top: 3rem;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 3rem;
    
    .page-title {
      font-size: 3rem;
      font-weight: 700;
      color: $text;
    }
  }

  .details {
    color: $light-gray-1;
    line-height: 1.6rem;
    font-size: 1.2rem;
    margin-bottom: 1rem;
  }

  .step {
    display: flex;
    flex-direction: column;
    margin-bottom: 2.5rem;

    .indicator {
      margin-bottom: 1rem;
    }

    .step-title {
      font-weight: 600;
      font-size: 1.2rem;
      margin-bottom: .75rem;
      text-align: center;
    }

    .couple-detail,
    .day-detail {
      display: flex;
      margin-bottom: 1rem;
      padding: 1rem;
      gap: .75rem;
      background: $dark-gray-2;
      border: 1px solid $light-gray-1;
      border-radius: .25rem; 

      .names {
        flex-grow: 1;
        display: flex;
        flex-direction: column;
        gap: .75rem;
        color: $text;
      }

      .action {
        display: flex;
        align-items: center;

        svg {
          height: 24px;
          fill: $dark-gray-1;
        }
      }
    }

    .couple-input {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-bottom: 1rem;

      .icon-input {
        display: flex;
        align-items: stretch;
        gap: .75rem;

        .icon {
          display: flex;
          align-items: center;
          /* padding: .75rem; */
          /* background: $dark-gray-1; */
          border-radius: .25rem;

          svg {
            height: 1.25rem;
            fill: $light-gray-2;
          }
        }

        input {
          width: 100%;
        }
      }
    }

    .day-input {
      margin-bottom: 1rem;
    }
  }

  .generate-attendance-list {
    margin-bottom: 2rem;
  }
}
</style>
