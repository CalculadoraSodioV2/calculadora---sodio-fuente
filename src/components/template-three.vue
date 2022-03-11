<template>
    <div>
    <div class="q-mt-md">
      {{ questionTwo }}
    </div>
    <div class="row q-mt-md">
      <div class="col-xs-12 col-sm-4">
        <q-card>
          <q-card-title class="text-center">
            {{ portionOne }}
          </q-card-title>
          <q-card-separator />
          <q-card-main>
            <div class="text-center">
                <q-radio v-model="portion" val="1" v-on:input="changeOptionValue('1')"/>
            </div>
            <div v-if="portion == '1'">
              <q-select
                v-model="select"
                :options="selectOptionsOne"
                @input="changeSelectValue()"
              />
            </div>
          </q-card-main>
        </q-card>
      </div>

      <div class="col-xs-12 col-sm-4">
        <q-card>
          <q-card-title class="text-center">
            {{ portionTwo }}
          </q-card-title>
          <q-card-separator />
          <q-card-main>
            <div class="text-center">
                <q-radio v-model="portion" val="2" v-on:input="changeOptionValue('2')"/>
            </div>
          </q-card-main>
        </q-card>
      </div>

      <div class="col-xs-12 col-sm-4">
        <q-card>
          <q-card-title class="text-center">
            {{ portionThree }}
          </q-card-title>
          <q-card-separator />
          <q-card-main>
            <div class="text-center">
                <q-radio v-model="portion" val="3" v-on:input="changeOptionValue('3')"/>
            </div>
            <div v-if="portion == '3'">
              <q-select
                v-model="select"
                :options="selectOptionsThree"
                @input="changeSelectValue()"
              />
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
    'questionTwo',
    'portionOne',
    'portionTwo',
    'portionThree',
    'selectOptionsOne',
    'selectOptionsThree',
    'active'
  ],
  data () {
    return {
      portion: '',
      select: '',
      label: 0,
      value: 0
    }
  },
  methods: {
    changeOptionValue (option) {
      this.option = option
      this.$emit('input', this.option)
    },
    changeSelectValue () {
      this.$emit('inputTwo', this.select)
    }
  }
}
</script>