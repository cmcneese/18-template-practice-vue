<template lang="html">
  <div class="">
    <section>
      <div class="container">
        <form class="panel" @submit.prevent="submitForm">
          <p class="panel-heading">Sign Up For My Web App</p>
          <div class="panel-block">
            <p class="control has-icon has-icon-left" v-for="form in formInputs">
              <template v-if="form.type === 'select'" v-model="formValues[form.id]">
                <span class="select is-fullwidth">
                  <select>
                    <option v-for="option in form.options">{{ option.label }}</option>
                  </select>
                </span>
              </template>

              <template v-else>
<template v-if="form.type === 'textarea'">
                  <textarea class="input textarea" :placeholder="form.label" v-model="formValues[form.id]"></textarea>
                  <i :class="form.icon" class="fa" aria-hidden="true"></i>
</template>

                <template v-else>
<input class="input" :placeholder="form.label" v-model="formValues[form.id]">
<i :class="form.icon" class="fa" aria-hidden="true"></i>
</template>
              </template>
            </p>
            <button class="button is-primary is-fullwidth">
              submit
            </button>
          </div>
        </form>
      </div>
    </section>
  </div>
</template>

<script>
const apiUrl = 'http://json-data.herokuapp.com/forms';
export default {
  data() {
    return {
      formInputs: [],
      formValues: {},
      apiUrl,
    };
  },
  mounted() {
    this.getData()
    this.submitForm();
  },
  methods: {
    getData() {
      fetch(this.apiUrl)
        .then((r) => r.json())
        .then((formInputs) => {
          this.formInputs = formInputs;
        });
    },
    submitForm(formValues) {
      console.log(this.formValues);
      fetch('http://tiny-tn.herokuapp.com/collections/form-isaac', {
        method: 'POST',
        headers: {
          'Accept': 'application/json',
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(this.formValues)
      });
    },
  },
};
</script>
