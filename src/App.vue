<template>
  <div class="container box my-4">

    <!-- singola linea -->
    <h1 class="text-center m-3">Password Generator</h1>
    <div class="input-group input-group-lg">

     
        <!-- <input id="numLenght" class="form-control" type="number" v-model="config.length" size="1"> -->
    
      <button class="btn btn-outline-secondary" @click="generate()" type="button">Generate</button>
      <button class="btn btn-outline-secondary" @click.prevent="copyToClipboard" type="button">Copy</button>
      
      <input type="text" class="form-control" v-on:focus="$event.target.select()" ref="generator" v-model="password" id="generator">
    </div>

    <div class="container my-4 text-center">
<!-- password Character -->
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" name="char_types_alpha_numeric" v-model="config.alphaNumeric" id="alpha_numeric">
        <label class="form-check-label" for="alpha_numeric">Alpha Numeric</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="checkbox" name="char_types_special_chars" v-model="config.specialChars" id="special_chars">
        <label class="form-check-label" for="special_chars">Special Chars</label>
      </div>



<!-- password case -->
      <div class="form-check form-check-inline">
        <input class="form-check-input" name="case" type="radio" id="uppercase" v-model="config.passwordCase" value="uppercase">
        <label class="form-check-label" for="uppercase">Upper Case</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" name="case" type="radio" id="lowercase" v-model="config.passwordCase" value="lowercase">
        <label class="form-check-label" for="lowercase">Lower Case</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" name="case" type="radio" id="mixedcase" v-model="config.passwordCase" value="mixedcase">
        <label class="form-check-label" for="mixedcase">Mixed Case</label>
      </div>


      <!-- password Lenght -->
    


    </div>
  </div> 
</template>

<script>
import Swal from 'sweetalert2';
export default {
  data() {
    return {
      password: '',
      config: {
        passwordCase: 'mixedcase',  // uppercase, lowercase, mixedcase,
        alphaNumeric: true,
        specialChars: true,    
        length: 12    
      },
    
    }

  },
  methods: {
    generate() {
      let pool = '';
      if (this.config.passwordCase == 'uppercase') {
        pool = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      } else if (this.config.passwordCase == 'lowercase') {
        pool = 'abcdefghijklmnopqrstuvwxyz';
      } else {
        pool = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
      }
      if (this.config.alphaNumeric) {
        pool += '1234567890';
      }
      if (this.config.specialChars) {
        pool += '?!@#$%&*-+/';
      }
      this.password = '';
      for (let i = 0; i < this.config.length; i++) {
        const randomIndex = Math.floor(Math.random() * pool.length);
        this.password += pool.charAt(randomIndex);
      }

    },
    copyToClipboard() {
      this.$refs.generator.focus();
      document.execCommand('copy');
      Swal.fire('Password Copied!', 'This is your new password: ' + this.password, 'success');
    },
  }
}
</script>


<style lang="scss" scoped>

.box {
  max-width: 800px;
}
</style>
