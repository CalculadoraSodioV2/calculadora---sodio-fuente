<template>
  <div>
    <div v-show="router == 0">
      <introduction
        @router="router = $event"
      ></introduction>
    </div>
    <div v-show="router == 1">
      <part-one
        @preguntas="preguntasParteUno = $event"
        @router="router = $event"
        @scroll="top = $event"
      ></part-one>
    </div>
    <div v-show="router == 2">
      <part-two
        @preguntas="preguntasParteDos = $event"
        @router="router = $event"
        @scroll="top = $event"
      ></part-two>
    </div>
    <div v-show="router == 3">
      <part-three
        @preguntas="preguntasParteTres = $event"
        @router="router = $event"
        @calculate="calculate = $event"
        @scroll="top = $event"
      ></part-three>
    </div>
    <div v-show="router == 4">
      <part-four
        @preguntas="preguntasParteCuatro = $event"
        @router="router = $event"
        @calculate="calculate = $event"
        @scroll="top = $event"
      ></part-four>
    </div>
    <div v-show="router > 4">
      <results
        :parteUno=preguntasParteUno
        :parteDos=preguntasParteDos
        :parteTres=preguntasParteTres
        :parteCuatro=preguntasParteCuatro
        :valores=porciones
        :calcular=calculate
        @scroll="top = $event"
        @exit="exit = $event"
      ></results>
    </div>
  </div>
</template>

<style>
</style>

<script>
import Introduction from './introduction.vue'
import PartOne from './PartOne.vue'
import PartTwo from './PartTwo.vue'
import PartThree from './PartThree.vue'
import PartFour from './PartFour.vue'
import Results from './Results.vue'

export default {
  name: 'PageIndex',
  data: function () {
    return {
      router: 0,
      preguntasParteUno: [],
      preguntasParteDos: [],
      preguntasParteTres: [],
      preguntasParteCuatro: [],
      porciones: [1150, 1178, 1229, 586, 744, 528, 286, 457, 340, 1754,
        850, 517, 1472, 673, 291, 2147, 2208, 1, 1257, 745,
        402, 663, 253, 564, 605, 945, 585, 700, 112, 82, 173,
        279, 193, 332, 118, 72, 281, 527, 506, 784, 901,
        124, 64, 100, 74, 193, 108, 132, 61, 137, 127,
        180, 261, 842, 846.5, 1003, 552, 201.5, 512, 456, 698,
        828, 539, 67, 511.5, 987, 656, 395.5, 1035, 326, 1 / 7,
        300],
      calculate: false,
      top: 0,
      exit: false,
      windows: ''
    }
  },
  methods: {
  },
  components: {
    'introduction': Introduction,
    'part-one': PartOne,
    'part-two': PartTwo,
    'part-three': PartThree,
    'part-four': PartFour,
    'results': Results
  },
  watch: {
    router: function () {
      scroll(0, 0)
    },
    exit: async function () {
      window.close()
    }
  },
  updated () {
    scroll(0, 0)
  }
}
</script>
