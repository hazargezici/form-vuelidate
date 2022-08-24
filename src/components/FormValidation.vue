<template>
  <div class="card">
    <div class="form-container">
      <div class="form-header">
        <h1>İletişim</h1>
      </div>
      <form>
        <div class="form-elements">
          <label>Adınız</label>
          <input
            class="pad"
            type="text"
            placeholder="Adınızı Giriniz"
            name=""
            id=""
            v-model.trim="$v.firstname.$model"
            :class="{
              'is-invalid': $v - firstname.$error,
              'is-valid': !$v.firstname.$invalid,
            }"
          />
          <div class="invalid-feedback">
            <span v-if="!$v.firstname.required">Adınız Boş Bırakılamaz *</span>
            <span v-if="!$v.firstname.minLength"
              >Adınız {{ $v.firstname.$params.minLength.min }} harften kısa
              olmamalıdır</span
            >
            <span v-if="!$v.firstname.maxLength"
              >Adınız {{ $v.firstname.$params.maxLength.max }} harften fazla
              olmalıdır</span
            >
          </div>
        </div>
        <div class="form-elements">
          <label>Soyadınız</label>
          <input
            type="text"
            placeholder="Soyadınızı Giriniz"
            name=""
            id=""
            v-model.trim="$v.lastname.$model"
            :class="{
              'is-invalid': $v - lastname.$error,
              'is-valid': !$v.lastname.$invalid,
            }"
          />
          <div class="invalid-feedback">
            <span v-if="!$v.lastname.required"
              >Soyadınız Boş Bırakılamaz *</span
            >
            <span v-if="!$v.lastname.minLength"
              >Soyadınız {{ $v.lastname.$params.minLength.min }} harften kısa
              olamamalıdır</span
            >
            <span v-if="!$v.lastname.maxLength"
              >soyadınız {{ $v.lastname.$params.maxLength.max }} harften uzun
              olmamlıdır</span
            >
          </div>
        </div>
        <div class="form-elements">
          <label>Yaşınız</label>
          <input
            type="number"
            name=""
            id=""
            v-model.number.lazy="$v.age.$model"
            :class="{
              'is-invalid': $v.age.$error,
              'is-valid': !$v.age.$invalid,
            }"
          />
          <div class="invalid-feedback">
            <span v-if="!$v.age.between"
              >Yaşınız {{ $v.age.$params.between.min }} ve
              {{ $v.age.$params.between.max }} arasında olmalıdır
            </span>
          </div>
        </div>
        <div class="form-elements">
          <label>Email</label>
          <input
            placeholder="Mail Adresinizi Giriniz"
            type="email"
            v-model.trim="$v.email.$model"
            :class="{
              'is-invalid': $v.email.$error,
              'is-valid': !$v.email.$invalid,
            }"
          />
          <div class="invalid-feedback">
            <span v-if="!$v.email.required">Email Boş Bırakılamaz *</span>
            <span v-if="!$v.email.email">Email geçerli olmalı</span>
          </div>
        </div>
        <div class="form-elemnts">
          <div class="number">
            <div class="phone">
              <label>Telefon</label>
              <PhoneMaskInput
                v-model="phone"
                autoDetectCountry
                @onValidate="onValidate"
                wrapperClass="wrraper-example"
                inputClass="input-example"
                class="phone-items"
              />

              <p class="json">{{ valid }}</p>
            </div>
          </div>
        </div>
        <div class="form-elements">
          <label>Şehir</label>
          <select
            name="sehir"
            v-model.trim="$v.şehir.$model"
            :class="{
              'is-invalid': $v - şehir.$error,
              'is-valid': !$v.şehir.$invalid,
            }"
          >
            <option>Kocaeli</option>
            <option>İstanbul</option>
            <option>Ankara</option>
            <option>İzmir</option>
            <option>Antalya</option>
          </select>
          <div class="invalid-feedback">
            <span v-if="!$v.şehir.required">Şehir Seçimi yapınız *</span>
          </div>
        </div>
        <div class="form-elements">
          <label>Adres</label>
          <textarea
            placeholder="Adresinizi Giriniz"
            cols="10"
            rows="2"
            v-model.trim="$v.adress.$model"
            :class="{
              'is-invalid': $v - adress.$error,
              'is-valid': !$v.adress.$invalid,
            }"
          ></textarea>
          <div class="invalid-feedback">
            <span v-if="!$v.adress.required">Adresinizi Giriniz *</span>
          </div>
        </div>

        <button type="submit">Gönder</button>
      </form>
    </div>
  </div>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  between,
  email,
  numeric,
} from "vuelidate/lib/validators";
import PhoneMaskInput from "vue-phone-mask-input";
export default {
  name: "FormValidation",
  data() {
    return {
      firstname: "",
      lastname: "",
      şehir: "",
      age: 0,
      email: "",
      phoneNumber: "",
      adress: "",
    };
  },
  validations: {
    firstname: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(10),
      numeric,
    },
    lastname: {
      required,
      minLength: minLength(3),
      maxLength: maxLength(10),
    },
    şehir: {
      required,
    },
    age: {
      required,
      between: between(18, 50),
      numeric,
    },
    email: {
      required,
      email,
    },
    phoneNumber: {
      required,
      numeric,
    },
    adress: {
      required,
    },
  },
  components: { PhoneMaskInput },
};
</script>

<style scoped>
.card {
  height: 120vh;
}
.form-container {
  display: flex;
  margin: auto;
  width: 40%;
  box-shadow: 5px 10px;
  border: 1px solid rgba(87, 87, 87, 0.281);
  margin-top: 50px;
}
.phone {
  margin-top: 20px;
}
.form-header {
  display: flex;
  align-items: center;
  width: 40%;
  background: linear-gradient(rgb(195, 160, 170), #9f1818);
}
.form-header h1 {
  margin: auto;
  color: #fff;
}
label {
  display: block;
  font-size: 20px;
}
.form-elements input,
select,
textarea {
  width: 100%;
  outline: none;
  border: 1px solid rgb(220, 217, 217);
  border-radius: 7px;
  padding: 10px;
  border-bottom-color: #9f1818;
  border-right-color: #9f1818;
}
.form-elements {
  margin-top: 8px;
  margin-left: 35px;
}
input {
  padding: 5px;
}
span {
  color: #c70808;
}
button {
  width: 95%;
  margin-left: 35px;
  margin-bottom: 20px;
  margin-top: 10px;
  padding: 10px 30px;
  border: none;
  background: linear-gradient(rgb(195, 160, 170), #bb4747);
  color: #fff;
  font-size: 25px;
  border-radius: 5px;
}
button:hover {
  cursor: pointer;
}
.number {
  margin-left: 35px;
  width: 100%;
}
</style>
