<template>
  <div>
    <div class="q-mt-md q-subheading" v-html="questionTwo">
      {{ questionTwo }}
    </div>
    <q-slider
      class="q-mt-md"
      v-model="option"
      :label-value="`${labelShowed()}`"
      :min="0"
      :max=max
      :step="1"
      label-always
      color="secondary"
      @change="scroll()"
      snap
      markers
    />
  </div>
</template>

<script>
export default {
  props: [
    'questionTwo',
    'label',
    'index',
    'ret'
  ],
  data () {
    return {
      option: 0,
      value: 0,
      max: 1
    }
  },
  methods: {
    labelShowed () {
      if (this.option === 0) {
        this.value = this.label[0].value
        return this.label[0].label
      }
      if (this.option === 1) {
        this.value = this.label[1].value
        return this.label[1].label
      }
      if (this.option === 2) {
        this.value = this.label[2].value
        return this.label[2].label
      }
      if (this.option === 3) {
        this.value = this.label[3].value
        return this.label[3].label
      }
      if (this.option === 4) {
        this.value = this.label[4].value
        return this.label[4].label
      }
      if (this.option === 5) {
        this.value = this.label[5].value
        return this.label[5].label
      }
      if (this.option === 6) {
        this.value = this.label[6].value
        return this.label[6].label
      }
      if (this.option === 7) {
        this.value = this.label[7].value
        return this.label[7].label
      }
      if (this.option === 8) {
        this.value = this.label[8].value
        return this.label[8].label
      }
      if (this.option === 9) {
        this.value = this.label[9].value
        return this.label[9].label
      }
      if (this.option === 10) {
        this.value = this.label[10].value
        return this.label[10].label
      }
      if (this.option === 11) {
        this.value = this.label[11].value
        return this.label[11].label
      }
      if (this.option === 12) {
        this.value = this.label[12].value
        return this.label[12].label
      }
      if (this.option === 13) {
        this.value = this.label[13].value
        return this.label[13].label
      }
      if (this.option === 14) {
        this.value = this.label[14].value
        return this.label[14].label
      }
      if (this.option === 15) {
        this.value = this.label[15].value
        return this.label[15].label
      }
      if (this.option === 16) {
        this.value = this.label[16].value
        return this.label[16].label
      }
      if (this.option === 17) {
        this.value = this.label[17].value
        return this.label[17].label
      }
      if (this.option === 18) {
        this.value = this.label[18].value
        return this.label[18].label
      }
      if (this.option === 19) {
        this.value = this.label[19].value
        return this.label[19].label
      }
      if (this.option === 20) {
        this.value = this.label[20].value
        return this.label[20].label
      }
    },
    scroll (index) {
      this.$emit('scroll', this.index)
    }
  },
  watch: {
    ret: function (newOption, oldOption) {
      this.value = newOption ? 0 : this.value
      this.option = newOption ? 0 : this.option
    },
    value: function () {
      this.$emit('input', this.value)
    }
  },
  mounted () {
    this.label.forEach((elem) => {
      this.max++
    })
    this.max--
    this.max--
  }
}
</script>
