<template>
  <div class="registration-form">
    <div class="left">
      <div class="title">
        <h1>Create your Account</h1>
      </div>
      <form @submit.prevent="handleSubmit" novalidate>
        <div class="form-input-group">
          <div class="form-input">
            <base-label label="First name" />
            <base-input placeholder="First name" v-model="input.firstName" :error="errors.firstName !== false" required />
            <span class="error" v-if="errors.firstName">{{ errors.firstName }}</span>
          </div>
          <div class="form-input">
            <base-label label="Last name" />
            <base-input placeholder="Last name" v-model="input.lastName" :error="errors.lastName !== false" required />
            <span class="error" v-if="errors.lastName">{{ errors.lastName }}</span>
          </div>
        </div>
        <div class="form-input">
          <base-label label="Email" />
          <base-input placeholder="Email" v-model="input.email" :error="errors.email !== false" required />
          <span class="error" v-if="errors.email">{{ errors.email }}</span>
        </div>
        <div class="form-input">
          <base-label label="Password" />
          <base-input placeholder="********" type="password" v-model="input.password" :error="errors.password !== false" required />
          <span class="error" v-if="errors.password">{{ errors.password }}</span>
        </div>
        <div class="form-select">
          <base-label label="Gender" />
          <base-select 
            placeholder="Select a gender" 
            v-bind:selected="input.gender" 
            :options="genderSelect.options" 
            v-on:update:selected="(value) => handleSelect('gender', value)" 
            :error="errors.gender !== false" 
            required 
          />
          <span class="error" v-if="errors.gender">{{ errors.gender }}</span>
        </div>
        <div class="form-select">
          <base-label label="Province" />
          <base-select 
            placeholder="Select a province" 
            v-bind:selected="input.province" 
            :options="provinceSelect.options" 
            v-on:update:selected="handleProvinceSelect" 
            :error="errors.province !== false" 
            required 
          />
          <span class="error" v-if="errors.province">{{ errors.province }}</span>
        </div>
        <div class="form-select">
          <base-label label="City" />
          <base-select 
            :placeholder="(input.province === '' && 'Select a province first') || 'Select a city'" 
            v-bind:selected="input.city" 
            :options="citySelect.optionToDisplay" 
            v-on:update:selected="(value) => handleSelect('city', value)" 
            :disabled="input.province === ''" 
            :error="errors.city !== false" 
            required 
          />
          <span class="error" v-if="errors.city">{{ errors.city }}</span>
        </div>
        <div class="button-container">
          <base-button name="Submit" />
        </div>
      </form>
    </div>
    <div class="right">
      <img src="../../assets/images/undraw_account_re_o7id.svg" />  
    </div>
  </div>
</template>

<script>
  import BaseLabel from '../atoms/BaseLabel.vue'
  import BaseInput from '../atoms/BaseInput.vue'
  import BaseSelect from '../atoms/BaseSelect.vue'
  import BaseButton from '../atoms/BaseButton.vue'

  export default {
    components: { BaseInput, BaseLabel, BaseSelect, BaseButton },
    data() {
      return {
        input: {
          firstName: '',
          lastName: '',
          email: '',
          password: '',
          gender: '',
          province: '',
          city: ''
        },
        errors: {
          firstName: false,
          lastName: false,
          email: false,
          password: false,
          gender: false,
          province: false,
          city: false
        },
        genderSelect: {
          options: [
            'Male',
            'Female',
            'Other',
            'Prefer not to answer'
          ]
        },
        provinceSelect: {
          selected: '',
          options: [
            'Aceh', 'Bali'
          ]
        },
        citySelect: {
          selected: '',
          optionToDisplay: [],
          options: [
            {
              id: 'Aceh',
              cities: [
                'Aceh Baray Regency', 'Aceh Barat Daya Regency', 'Aceh Besar Regency', 'Aceh Jaya Regency', 'Aceh Selatan Regency',
              ]
            },
            {
              id: 'Bali',
              cities: [
                'Denpasar', 'Jimbaran', 'Kuta', 'Pecatu', 'Ubud'
              ]
            }
          ]
        }
      }
    },
    methods: {
      handleSubmit() {
        this.errors.firstName = this.input.firstName.length > 0 ? false : "This field cannot be empty";
        this.errors.lastName = this.input.lastName.length > 0 ? false : "This field cannot be empty";
        
        if(this.input.email.length > 0) {
          this.errors.email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.input.email) ? false : "You have entered an invalid email address";
        } else {
          this.errors.email = "This field cannot be empty";
        }

        this.errors.password = this.input.password.length > 0 ? false : "This field cannot be empty";
        this.errors.gender = this.input.gender.length > 0 ? false : "This field cannot be empty";
        this.errors.province = this.input.province.length > 0 ? false : "This field cannot be empty";
        this.errors.city = this.input.city.length > 0 ? false : "This field cannot be empty";

        if(Object.values(this.errors).every(value => value === false)) {
          this.$router.push('/login');
        }
      },
      handleSelect(selected, value) {
        this.input[selected] = value;
      },
      handleProvinceSelect(value) {
        this.input.province = value;
        this.citySelect.optionToDisplay = this.filterCityList();
      },
      filterCityList() {
        return this.citySelect.options.filter(province => {
          return province.id === this.input.province;
        })[0].cities;
      }
    }
  }
</script>

<style lang="scss">
  .registration-form {
    display: flex;
    justify-content: space-evenly;
    align-items: center;
    margin-block: 50px;

    .right {
      display: flex;
      align-items: center;

      img {
        width: 30vw;
      }
    }

    .title {
      margin-bottom: 15px;

      h1 {
        font-style: normal;
        font-weight: 500;
        font-size: 30px;
      }
    }

    form {
      display: flex;
      flex-direction: column;
      row-gap: 10px;
      z-index: 0;

      .form-input-group {
        display: flex;
        justify-content: space-between;
        column-gap: 20px;
      }

      .form-input {
        display: flex;
        flex-direction: column;
      }

      .form-select {
        display: flex;
        flex-direction: column;
      }

      .error {
        font-size: 14px;
        color: #D51A52;
        text-align: right;
      }

      .button-container {
        width: 100%;
        margin-top: 20px;
      }
    }
  }

  @media screen and (max-width: 1024px) {
    .registration-form {
      margin: 0;

      .right {
        display: none;
      }
    }
  }

  @media screen and (max-width: 480px) {
    .registration-form {
      margin-block: 10px;

      .title {
        width: 100%;
        display: flex;
      }

      form {
        width: 100%;

        .form-input-group {
          display: flex;
          flex-direction: column;
          row-gap: 10px;
        }
      }

      .right {
        display: none;
      }
    }
  }
</style>