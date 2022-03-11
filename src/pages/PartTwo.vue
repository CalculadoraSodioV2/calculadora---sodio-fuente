<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-headline text-white">
            II. COMIDA TIPO CASERA Y ANTOJITOS MEXICANOS <br /><br />
            SECCIÓN 2 DE 4
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading text-weight-bold q-mt-md bg-teal-1 q-pa-md">
            Díganos con qué frecuencia come comida casera preparada por alguien más, comida tipo casera en cocinas económicas (fondas) o comedores en su lugar de trabajo. También, díganos con qué frecuencia consume antojitos mexicanos, ya sea en establecimientos ambulantes o fijos, incluyendo cafeterías o restaurantes.
          </div>

          <div v-for="pregunta in variablesPreguntas" v-bind:key="pregunta.id" class="q-mt-xl">
            <div class="q-headline q-mt-lg text-weight-bold text-secondary" v-if="pregunta.seccion != ''">
              {{ pregunta.seccion }}
            </div>

            <template-one
                        :question=pregunta.pregunta
                        v-model="preguntas[pregunta.id]"
                        :numero=pregunta.numero>
            </template-one>
            <q-slide-transition>
              <template-two v-show="preguntas[pregunta.id] != 1"
                          :questionTwo=pregunta.parteDos
                          :label=pregunta.opciones
                          :ret=returnToZero[pregunta.id]
                          v-model="porciones[pregunta.id]">
              </template-two>
            </q-slide-transition>
          </div>

          <div class="row reverse">
            <q-btn-group class="q-mt-xl">
              <q-btn label="Regresar"
                color="light"
                size="lg"
                @click="previousPage()"/>
              <q-btn label="Continuar"
                color="secondary"
                size="lg"
                @click="nextPage()"/>
            </q-btn-group>
          </div>
        </q-card-main>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import templateOne from '../components/template-one.vue'
import templateTwo from '../components/template-two.vue'

export default {
  name: 'PartTwo',
  data () {
    return {
      variablesPreguntas: [
        {
          id: 0,
          numero: 18,
          seccion: 'Comida tipo casera',
          pregunta: `<span class="text-weight-bold">Comida casera preparada <u>por alguien que no sea usted</u> o tipo casera (comida corrida en cocinas económicas 
                    o en el comedor de su lugar de trabajo).</span>`,
          parteDos: `<span class="text-weight-bold">18a.&nbsp Cuando consume comida tipo casera en cocinas económicas o en su 
                    lugar de trabajo ¿qué come habitualmente? </span><br/>
                    &nbsp &nbsp &nbsp La <u>sopa aguada incluye</u> pasta en caldillo, sopas y cremas de verduras o consomé. 
                    La <u>sopa seca incluye</u> arroz (rojo, blanco, amarillo, verde, etc.) o pasta seca (espagueti, coditos, etc.). En todos los 
                    casos considere las porciones tal y como se sirven. `,
          opciones: [
            {
              label: 'Sopa aguada + guisado',
              value: 887 + 902
            },
            {
              label: 'Sopa seca + guisado',
              value: 717 + 902
            },
            {
              label: 'Sopa aguada + sopa seca + guisado',
              value: 887 + 717 + 902
            }
          ]
        },
        {
          id: 1,
          numero: 19,
          seccion: 'Antojitos mexicanos',
          pregunta: `<span class="text-weight-bold">Pambazos o tortas de milanesa, jamón, salchicha, pierna, cubana, etc., en establecimientos ambulantes o fijos.`,
          parteDos: `<span class="text-weight-bold">19a.&nbsp Cuando come pambazos o tortas ¿cuántas piezas consume habitualmente?</span> `,
          opciones: [
            {
              label: 'Menos de 1 pambazo o torta',
              value: 0.25
            },
            {
              label: 'La mitad de 1 pambazo o torta',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 pambazo o torta',
              value: 0.75
            },
            {
              label: '1 pambazo o torta',
              value: 1
            },
            {
              label: '1 1/2 pambazos o tortas',
              value: 1.5
            },
            {
              label: '2 pambazos o tortas',
              value: 2
            },
            {
              label: '3 pambazos o tortas',
              value: 3
            },
            {
              label: '4 pambazos o tortas',
              value: 4
            },
            {
              label: '5 pambazos o tortas',
              value: 5
            },
            {
              label: '6 pambazos o tortas',
              value: 6
            },
            {
              label: '7 pambazos o tortas',
              value: 7
            },
            {
              label: '8 pambazos o tortas',
              value: 8
            },
            {
              label: '9 pambazos o tortas',
              value: 9
            }
          ]
        },
        {
          id: 2,
          seccion: '',
          numero: 20,
          pregunta: `<span class="text-weight-bold">Tostadas de pata o tinga en establecimientos ambulantes o fijos.</span>`,
          parteDos: `<span class="text-weight-bold">20a.&nbsp Cuando come tostadas ¿cuántas piezas consume habitualmente?</span> `,
          opciones: [
            {
              label: '1 tostada',
              value: 1
            },
            {
              label: '2 tostadas',
              value: 2
            },
            {
              label: '3 tostadas',
              value: 3
            },
            {
              label: '4 tostadas',
              value: 4
            },
            {
              label: '5 tostadas',
              value: 5
            },
            {
              label: '6 tostadas',
              value: 6
            },
            {
              label: '7 tostadas',
              value: 7
            },
            {
              label: '8 tostadas',
              value: 8
            },
            {
              label: '9 tostadas',
              value: 9
            }
          ]
        },
        {
          id: 3,
          seccion: '',
          numero: 21,
          pregunta: `<span class="text-weight-bold">Sopes sencillos o con guisado, quesadillas o tlacoyos, en establecimientos ambulantes o fijos.</span>`,
          parteDos: `<span class="text-weight-bold">21a.&nbsp Cuando come sopes, quesadillas o tlacoyos ¿cuántas piezas consume habitualmente?</span> `,
          opciones: [
            {
              label: '1 pieza',
              value: 1
            },
            {
              label: '2 piezas',
              value: 2
            },
            {
              label: '3 piezas',
              value: 3
            },
            {
              label: '4 piezas',
              value: 4
            },
            {
              label: '5 piezas',
              value: 5
            },
            {
              label: '6 piezas',
              value: 6
            },
            {
              label: '7 piezas',
              value: 7
            },
            {
              label: '8 piezas',
              value: 8
            },
            {
              label: '9 piezas',
              value: 9
            }
          ]
        },
        {
          id: 4,
          seccion: '',
          numero: 22,
          pregunta: `<span class="text-weight-bold">Gorditas de chicharrón o tacos de carnitas en establecimientos ambulantes o fijos.</span>`,
          parteDos: `<span class="text-weight-bold">22a.&nbsp Cuando come gorditas o tacos de carnitas ¿cuántas piezas consume habitualmente?</span> `,
          opciones: [
            {
              label: 'Menos de la mitad de 1 gordita o taco',
              value: 0.25
            },
            {
              label: 'La mitad de 1 gordita o taco',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 gordita o taco',
              value: 0.75
            },
            {
              label: '1 gordita o taco',
              value: 1
            },
            {
              label: '1 1/2 gorditas o tacos',
              value: 1.5
            },
            {
              label: '2 gorditas o tacos',
              value: 2
            },
            {
              label: '3 gorditas o tacos',
              value: 3
            },
            {
              label: '4 gorditas o tacos',
              value: 4
            },
            {
              label: '5 gorditas o tacos',
              value: 5
            },
            {
              label: '6 gorditas o tacos',
              value: 6
            },
            {
              label: '7 gorditas o tacos',
              value: 7
            },
            {
              label: '8 gorditas o tacos',
              value: 8
            },
            {
              label: '9 gorditas o tacos',
              value: 9
            }
          ]
        },
        {
          id: 5,
          seccion: '',
          numero: 23,
          pregunta: `<span class="text-weight-bold">Tacos en establecimientos ambulantes o fijos.</span><br/>
                    <span class="text-weight-light">P. ej., de canasta (sudados de papa, papa con bistec o longaniza, frijol o chicharrón), bistec, suadero, 
                    al pastor, tripa, barbacoa, flautas de barbacoa, etc.</span>`,
          parteDos: `<span class="text-weight-bold">23a.&nbsp Cuando come tacos ¿cuántas piezas consume habitualmente?</span> `,
          opciones: [
            {
              label: '1 taco',
              value: 1
            },
            {
              label: '2 tacos',
              value: 2
            },
            {
              label: '3 tacos',
              value: 3
            },
            {
              label: '4 tacos',
              value: 4
            },
            {
              label: '5 tacos',
              value: 5
            },
            {
              label: '6 tacos',
              value: 6
            },
            {
              label: '7 tacos',
              value: 7
            },
            {
              label: '8 tacos',
              value: 8
            },
            {
              label: '9 tacos',
              value: 9
            }
          ]
        },
        {
          id: 6,
          seccion: '',
          numero: 24,
          pregunta: `<span class="text-weight-bold">Tamales en establecimientos ambulantes o fijos, o bien empaquetados o congelados del supermercado o tiendas de conveniencia.</span><br/>
                    <span class="text-weight-light">P. ej., tamales de cualquier sabor o salsa, en hoja de maíz o de plátano (oaxaqueños).</span>`,
          parteDos: `<span class="text-weight-bold">24a.&nbsp Cuando come tamales ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 tamal',
              value: 0.25
            },
            {
              label: 'La mitad de 1 tamal',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 tamal',
              value: 0.75
            },
            {
              label: '1 tamal',
              value: 1
            },
            {
              label: '1 1/2 tamales',
              value: 1.5
            },
            {
              label: '2 tamales',
              value: 2
            },
            {
              label: '3 tamales',
              value: 3
            },
            {
              label: '4 tamales',
              value: 4
            },
            {
              label: '5 tamales',
              value: 5
            },
            {
              label: '6 tamales',
              value: 6
            },
            {
              label: '7 tamales',
              value: 7
            },
            {
              label: '8 tamales',
              value: 8
            },
            {
              label: '9 tamales',
              value: 9
            }
          ]
        },
        {
          id: 7,
          seccion: '',
          numero: 25,
          pregunta: `<span class="text-weight-bold">Burritos en establecimientos ambulantes o fijos, o bien empaquetados o congelados del supermercado o tiendas de conveniencia.</span><br/>
                    <span class="text-weight-light">P. ej., burritos de carne con frijol y queso, chicharrón con frijol y queso, frijol con queso, etc.</span>`,
          parteDos: `<span class="text-weight-bold">25a.&nbsp Cuando come burritos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 burrito',
              value: 0.25
            },
            {
              label: 'La mitad de 1 burrito',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 burrito',
              value: 0.75
            },
            {
              label: '1 burrito',
              value: 1
            },
            {
              label: '1 1/2 burritos',
              value: 1.5
            },
            {
              label: '2 burritos',
              value: 2
            },
            {
              label: '3 burritos',
              value: 3
            },
            {
              label: '4 burritos',
              value: 4
            },
            {
              label: '5 burritos',
              value: 5
            },
            {
              label: '6 burritos',
              value: 6
            },
            {
              label: '7 burritos',
              value: 7
            },
            {
              label: '8 burritos',
              value: 8
            },
            {
              label: '9 burritos',
              value: 9
            }
          ]
        },
        {
          id: 8,
          seccion: '',
          numero: 26,
          pregunta: `<span class="text-weight-bold">Enchiladas o chilaquiles en establecimientos ambulantes o fijos, o bien empaquetados o 
                    congelados del supermercado o tiendas de conveniencia. No considere las enchiladas o chilaquiles 
                    incluidos como plato principal (guisado) en una comida corrida.  </span>`,
          parteDos: `<span class="text-weight-bold">26a.&nbsp Cuando come enchiladas o chilaquiles ¿cuántas órdenes consume habitualmente? 
                    Una orden equivale a 3 piezas de enchiladas o 1 taza de chilaquiles.</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 orden',
              value: 0.25
            },
            {
              label: 'La mitad de 1 orden',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 orden',
              value: 0.75
            },
            {
              label: '1 orden',
              value: 1
            },
            {
              label: '1 1/2 órdenes',
              value: 1.5
            },
            {
              label: '2 órdenes',
              value: 2
            },
            {
              label: '3 órdenes',
              value: 3
            },
            {
              label: '4 órdenes',
              value: 4
            },
            {
              label: '5 órdenes',
              value: 5
            },
            {
              label: '6 órdenes',
              value: 6
            },
            {
              label: '7 órdenes',
              value: 7
            },
            {
              label: '8 órdenes',
              value: 8
            },
            {
              label: '9 órdenes',
              value: 9
            }
          ]
        }
      ],
      preguntas: [],
      porciones: [],
      respuestas: [],
      returnToZero: []
    }
  },
  methods: {
    nextPage () {
      this.$emit('preguntas', this.respuestas)
      this.$emit('router', 3)
    },
    previousPage () {
      this.$emit('router', 1)
    },
    setAnwers () {
      this.preguntas.forEach((pregunta, index) => {
        this.returnToZero[index] = false
        if (pregunta === '1') {
          this.returnToZero[index] = true
          this.respuestas[index] = {
            dia: 0,
            porcion: 0
          }
        }
        if (pregunta === '2') {
          this.respuestas[index] = {
            dia: 35 / 3650,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '3') {
          this.respuestas[index] = {
            dia: 90 / 3650,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '4') {
          this.respuestas[index] = {
            dia: 10 / 300,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '5') {
          this.respuestas[index] = {
            dia: 25 / 300,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '6') {
          this.respuestas[index] = {
            dia: 1 / 7,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '7') {
          this.respuestas[index] = {
            dia: 2 / 7,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '8') {
          this.respuestas[index] = {
            dia: 35 / 70,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '9') {
          this.respuestas[index] = {
            dia: 55 / 70,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '10') {
          this.respuestas[index] = {
            dia: 1,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '11') {
          this.respuestas[index] = {
            dia: 2.5,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '12') {
          this.respuestas[index] = {
            dia: 4.5,
            porcion: this.porciones[index]
          }
        }
        if (pregunta === '13') {
          this.respuestas[index] = {
            dia: 6,
            porcion: this.porciones[index]
          }
        }
      })
    },
    start () {
      for (let i = 0; i < 9; i++) {
        this.preguntas[i] = '1'
        this.returnToZero[i] = false
      }
    }
  },
  components: {
    'template-one': templateOne,
    'template-two': templateTwo
  },
  watch: {
    preguntas: function () {
      this.setAnwers()
    },
    porciones: function () {
      this.setAnwers()
    }
  },
  mounted () {
    this.start()
  }
}
</script>

<style>
</style>
