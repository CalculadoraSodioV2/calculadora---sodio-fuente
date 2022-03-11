<template>
  <div>
    <div class="q-mt-sm q-subheading">
        <ol>
          <li :value=numero class="text-weight-bold"><span v-html="question"></span></li>
        </ol>
    </div>
    <div class="row q-mt-md">
      <div class="col-xs-12 col-sm-6 col-md-3">
        <q-card>
          <q-card-title class="text-center q-pa-xs">
            <span class="q-subheading ">Al año</span>
          </q-card-title>
          <q-card-separator />
          <q-card-main class="q-pa-sm">
            <div class="row">
              <div class="col-4 text-center">
                Nunca
              </div>
              <div class="col-4 text-center">
                1-6
              </div>
              <div class="col-4 text-center">
                7-11
              </div>
              <div class="col-4 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('1')" val="1" color="orange-10"/>
              </div>
              <div class="col-4 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('2')" val="2" color="orange-10"/>
              </div>
              <div class="col-4 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('3')" val="3" color="orange-10"/>
              </div>
            </div>
          </q-card-main>
        </q-card>
      </div>

      <div class="col-xs-12 col-sm-6 col-md-3">
        <q-card>
          <q-card-title class="text-center q-pa-xs">
            <span class="q-subheading">Al mes</span>
          </q-card-title>
          <q-card-separator />
          <q-card-main class="q-pa-sm">
            <div class="row">
              <div class="col-6 text-center">
                1
              </div>
              <div class="col-6 text-center">
                2-3
              </div>
              <div class="col-6 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('4')" val="4" color="orange-10"/>
              </div>
              <div class="col-6 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('5')" val="5" color="orange-10"/>
              </div>
            </div>
          </q-card-main>
        </q-card>
      </div>

      <div class="col-xs-12 col-sm-6 col-md-3">
        <q-card>
          <q-card-title class="text-center q-pa-xs">
            <span class="q-subheading">A la semana</span>
          </q-card-title>
          <q-card-separator />
          <q-card-main class="q-pa-sm">
            <div class="row">
              <div class="col-3 text-center">
                1
              </div>
              <div class="col-3 text-center">
                2
              </div>
              <div class="col-3 text-center">
                3-4
              </div>
              <div class="col-3 text-center">
                5-6
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('6')" val="6" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('7')" val="7" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('8')" val="8" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('9')" val="9" color="orange-10"/>
              </div>
            </div>
          </q-card-main>
        </q-card>
      </div>

      <div class="col-xs-12 col-sm-6 col-md-3">
        <q-card>
          <q-card-title class="text-center q-pa-xs">
            <span class="q-subheading">Al día</span>
          </q-card-title>
          <q-card-separator />
          <q-card-main class="q-pa-sm">
            <div class="row">
              <div class="col-3 text-center">
                1
              </div>
              <div class="col-3 text-center">
                2-3
              </div>
              <div class="col-3 text-center">
                4-5
              </div>
              <div class="col-3 text-center">
                6 o más
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('10')" val="10" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('11')" val="11" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('12')" val="12" color="orange-10"/>
              </div>
              <div class="col-3 text-center">
                <q-radio v-bind:value="option" v-on:input="changeOptionValue('13')" val="13" color="orange-10"/>
              </div>
            </div>
          </q-card-main>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'question',
    'numero'
  ],
  data () {
    return {
      option: '1'
    }
  },
  methods: {
    changeOptionValue (option) {
      this.option = option
      this.$emit('input', this.option)
    }
  }
}
</script>
