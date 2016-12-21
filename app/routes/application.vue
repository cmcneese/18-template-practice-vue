<template lang="html">
  <div class="">
<div class="section page">
<form @submit.prevent="submitForm" class="panel">
  <div class="panel-heading">
    <h2>Sign Up For My Web App</h2>
    </div>
    <div class="panel-block">
      <p class="control has-icon" v-for="formInput in formInputs">
      <template v-if="formInput.type === 'select'">
          <span class="select is-fullwidth">
            <select v-model="formValues[formInput.id]">
              <option :value="undefined">{{formInput.label}}</option>
              <option v-for="option in formInput.options">
                {{ option.label }}
              </option>
            </select>
          </span>
      </template>

      <template v-else>
<template v-if="formInput.type === 'textarea'">
          <textarea class="textarea input"
            type="textarea"
            :placeholder="formInput.label"
            v-model="formValues[formInput.id]"></textarea>
          <i :class="formInput.icon" class="fa" aria-hidden="true"></i>
</template>
        <template v-else>
<input class="input" :placeholder="formInput.label" v-model="formValues[formInput.id]">
<i :class="formInput.icon" class="fa" aria-hidden="true"></i>
</template>
      </template>
      </p>
    </div>
      <div class="panel-block">
    <button class="button is-primary is-fullwidth">Submit</button>
  </div>
    </form>
      </div>
  </div>
</template>

<script>
const apiUrl = 'http://json-data.herokuapp.com/forms';

export default {
  data() {
    return {
      apiUrl,
      formInputs: [],
      formValues: {},
    };
  },

  mounted() {
    this.getData();
  },

  methods: {
    getData() {
      fetch(apiUrl)
        .then((r) => r.json())
        .then((formInputs) => {
          console.log(formInputs);
          this.formInputs = formInputs;
          console.log(formInputs);
        });
    },

    submitForm(formValues) {
      fetch('http://tiny-tn.herokuapp.com/collections/form-shaun', {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(this.formValues)
      });

  },

},
};
</script>
