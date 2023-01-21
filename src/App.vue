<template>
 <main>
  <div class="card-image-section">
    <picture class="background-image">
      <source srcset="./assets/bg-main-desktop.png" media="(min-width: 768px)">
      <img src="./assets/bg-main-mobile.png" alt="">
    </picture>
    <div class="card-front">
      <img src="./assets/bg-card-front.png" alt="">
      <p class="card-number-text">{{ cardNumber ? cardNumber : '1234 5678 9123 0000' }}</p>
      <p class="cardholder-name-text">{{ cardholderName ? cardholderName : 'Surajit Maity' }}</p>
      <p class="exp-date-text">{{ (expDateMonth ? expDateMonth : '00') + '/' + (expDateYear ? expDateYear : '00') }}</p>
    </div>
    <div class="card-back">
      <img src="./assets/bg-card-back.png" alt="">
      <p class="cvv-text">{{ cvv ? cvv : '123' }}</p>
    </div>
  </div>
  <div v-if="!isFormSubmited" class="card-info-section">
    <form class="card-form" @submit.prevent="handleSubmit">
      <div class="form-field">
        <label for="cardholder-name" class="field-name">CARDHOLDER NAME</label>
        <input type="text" id="cardholder-name" placeholder="e.g. Surajit Maity" v-model="cardholderName" :class="cardholderNameErrorMsg ? 'errorFiled' : ''">
        <p v-if="cardholderNameErrorMsg" class="error-msg">{{ cardholderNameErrorMsg }}</p>
      </div>
      <div class="form-field">
        <label for="card-number" class="field-name">CARD NUMBER</label>
        <input type="text" id="card-number" placeholder="e.g. 1234 5678 9123 0000" v-model="cardNumber" :class="cardNumberErrorMsg ? 'errorFiled' : ''">
        <p v-if="cardNumberErrorMsg" class="error-msg">{{ cardNumberErrorMsg }}</p>
      </div>
      <div class="last-field-group">
        <div class="form-field">
          <label for="exp-date" class="field-name">EXP. DATE (MM/YY)</label>
          <div class="exp-date-inputs">
            <input type="text" id="exp-date" placeholder="MM" v-model="expDateMonth" :class="expDateErrorMsg ? 'errorFiled' : ''">
            <input type="text" placeholder="YY" v-model="expDateYear" :class="expDateErrorMsg ? 'errorFiled' : ''">
          </div>
          <p v-if="expDateErrorMsg" class="error-msg">{{ expDateErrorMsg }}</p>
        </div>
        <div class="form-field">
          <label for="cvv" class="field-name">CVV</label>
          <input type="text" id="cvv" placeholder="e.g. 123" v-model="cvv" :class="cvvErrorMsg ? 'errorFiled' : ''">
          <p v-if="cvvErrorMsg" class="error-msg">{{ cvvErrorMsg }}</p>
        </div>
      </div>
      <button>Confirm</button>
    </form>
  </div>
  <div v-if="isFormSubmited" class="thank-you-section">
    <img src="./assets/icon-complete.svg" alt="">
    <p class="thank-you-heading">THANK YOU!</p>
    <p class="thank-you-description">We added your card details.</p>
    <button>Continue</button>
  </div>
 </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      cardholderName: '',
      cardNumber: '',
      expDateMonth: '',
      expDateYear: '',
      cvv: '',
      isFormSubmited: false,
      cardholderNameErrorMsg: '',
      cardNumberErrorMsg: '',
      expDateErrorMsg: '',
      cvvErrorMsg: '',
    };
  },
  methods: {
    handleSubmit() {
      this.validateForm();
      if(!this.cardholderNameErrorMsg && !this.cardNumberErrorMsg && !this.expDateErrorMsg && !this.cvvErrorMsg) {
        this.isFormSubmited = true;
      }
    },
    validateForm() {
      this.validateCardholderName();
      this.validateCardNumber();
      this.validateExpDate();
      this.validateCvv();
    },
    validateCardholderName() {
      if(!this.cardholderName) {
        this.cardholderNameErrorMsg = "Can't be blank";
      } else {
        this.cardholderNameErrorMsg = '';
      }
    },
    validateCardNumber() {
      if(!this.cardNumber) {
        this.cardNumberErrorMsg = "Can't be blank";
      } else {
        this.cardNumberErrorMsg = '';
      }
    },
    validateExpDate() {
      if(!this.expDateMonth || !this.expDateYear) {
        this.expDateErrorMsg = "Can't be blank";
      } else {
        this.expDateErrorMsg = '';
      }
    },
    validateCvv() {
      if(!this.cvv) {
        this.cvvErrorMsg = "Can't be blank";
      } else {
        this.cvvErrorMsg = '';
      }
    },
  },
  watch: {
    cardholderName() {
      this.validateCardholderName();
    },
    cardNumber() {
      this.validateCardNumber();
    },
    expDateMonth() {
      this.validateExpDate();
    },
    expDateYear() {
      this.validateExpDate();
    },
    cvv() {
      this.validateCvv();
    },
  },
}
</script>
