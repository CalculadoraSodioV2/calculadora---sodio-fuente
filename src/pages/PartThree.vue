<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-headline text-white">
            III. HELADOS, POSTRES, RESPOSTERÍA, PANADERÍA Y GALLETAS <br /><br />
            SECCIÓN 3 DE 4
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading text-weight-bold q-mt-md bg-teal-1 q-pa-md">
            Díganos con qué frecuencia come postres, helados, productos de repostería, panadería y galletas.
          </div>

          <div v-for="pregunta in variablesPreguntas" v-bind:key="pregunta.id" class="q-mt-xl">
            <div class="q-headline q-mt-lg text-secondary" v-if="pregunta.seccion != ''">
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
  name: 'PartThree',
  data () {
    return {
      variablesPreguntas: [
        {
          id: 0,
          seccion: '',
          numero: 27,
          pregunta: `<span class="text-weight-bold">Helados de crema y pasteles de helado de crema de restaurantes de comida rápida o cadenas de heladerías (p.ej., McDonald’s, Burger King, Dairy Queen, etc.) </span>`,
          parteDos: `<span class="text-weight-bold">27a.&nbsp Cuando toma helados de crema o come pasteles de helado de crema 
                    ¿cuántas piezas consume habitualmente? Considere como una pieza 1 helado mediano o estándar, o 1 rebanada de pastel  de helado</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de una pieza',
              value: 0.25
            },
            {
              label: 'La mitad de una pieza',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de una pieza',
              value: 0.75
            },
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
          id: 1,
          seccion: '',
          numero: 28,
          pregunta: `<span class="text-weight-bold">Malteadas, smoothies o frappés en establecimientos de comida rápida, restaurantes o cafeterías en su barrio o colonia 
                    (p.ej., Carl´s Jr, Dairy Queen, Mc Donald´s, Starbucks, Burger King, etc.) <u>No</u> considere los frappés a base de café o té, 
                    ya que éstos se preguntan más adelante. </span>`,
          parteDos: `<span class="text-weight-bold">28a.&nbsp Cuando toma malteadas, smoothies o frappés ¿cuántas bebidas consume habitualmente? 
                    Considere una bebida como una pieza de tamaño mediano o estándar.</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de una bebida',
              value: 0.25
            },
            {
              label: 'La mitad de una bebida',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de una bebida',
              value: 0.75
            },
            {
              label: '1 bebida',
              value: 1
            },
            {
              label: '2 bebidas',
              value: 2
            },
            {
              label: '3 bebidas',
              value: 3
            }
          ]
        },
        {
          id: 2,
          seccion: '',
          numero: 29,
          pregunta: `<span class="text-weight-bold"> Bebidas a base de café, té o chocolate, calientes o frías, en establecimientos de comida rápida, 
                    restaurantes o cafeterías en su barrio o colonia (p.ej., Italian Coffee, Starbucks, Krispy Kreme, Mc Donald´s, etc.)</span>. No considere el café, infusiones o té preparados solamente con agua.<br/>
                    <span class="text-weight-light">P. ej., café latte, moka, capuccino, chai late, frappé de café, frappé de té verde o té chai, chocolate caliente, chocolate frío, moka blanco, etc.</span>`,
          parteDos: `<span class="text-weight-bold">29a.&nbsp Cuando toma bebidas a base de café, té o chocolate, calientes o frías ¿cuántas bebidas 
                    consume habitualmente? Considere una bebida como una pieza de tamaño mediano o estándar</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 bebida',
              value: 0.25
            },
            {
              label: 'La mitad de una bebida',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de una bebida',
              value: 0.75
            },
            {
              label: '1 bebida',
              value: 1
            },
            {
              label: '2 bebidas',
              value: 2
            },
            {
              label: '3 bebidas',
              value: 3
            }
          ]
        },
        {
          id: 3,
          seccion: '',
          numero: 30,
          pregunta: `<span class="text-weight-bold">Postres tipo flan, gelatina de leche, natilla, arroz con leche o chongos zamoranos, ya sean empaquetados, preparados a partir de 
                    polvos o en restaurantes o algún otro establecimiento en su barrio o colonia. </span>`,
          parteDos: `<span class="text-weight-bold">30a.&nbsp Cuando come alguno de estos postres ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1/2 taza',
              value: 0.5
            },
            {
              label: '1/2 taza',
              value: 1
            },
            {
              label: '3/4 de taza',
              value: 1.5
            },
            {
              label: '1 taza',
              value: 2
            },
            {
              label: '2 tazas',
              value: 4
            },
            {
              label: '3 tazas',
              value: 6
            },
            {
              label: '4 tazas',
              value: 8
            },
            {
              label: '5 tazas',
              value: 10
            },
            {
              label: '6 tazas',
              value: 12
            },
            {
              label: '7 tazas',
              value: 14
            },
            {
              label: '8 tazas',
              value: 16
            },
            {
              label: '9 tazas',
              value: 18
            }
          ]
        },
        {
          id: 4,
          seccion: '',
          numero: 31,
          pregunta: `<span class="text-weight-bold">Productos de panadería como muffins, donas, panqués, pan de canela, churros y pan dulce variado; 
                    ya sean empaquetados, elaborados en casa a base de harinas preparadas, de panadería, restaurantes, cafeterías o algún otro establecimiento en su barrio o colonia.</span>`,
          parteDos: `<span class="text-weight-bold">31a.&nbsp Cuando come alguno de estos productos de panadería dulce ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 pieza',
              value: 0.25
            },
            {
              label: 'La mitad de 1 pieza',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 pieza',
              value: 0.75
            },
            {
              label: '1 pieza',
              value: 1
            },
            {
              label: '1 1/2 piezas',
              value: 1.5
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
          id: 5,
          seccion: '',
          numero: 32,
          pregunta: `<span class="text-weight-bold">Productos de repostería como pasteles, tartas, pays o brownies; ya sean empaquetados, congelados, elaborados en casa a partir de harinas preparadas, de panadería, 
                    restaurantes, cafeterías o algún otro establecimiento en su barrio o colonia. </span>`,
          parteDos: `<span class="text-weight-bold">32a.&nbsp Cuando come alguno de estos productos de repostería ¿cuántas piezas individuales o rebanadas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 pieza o rebanada',
              value: 0.25
            },
            {
              label: 'La mitad de 1 pieza o rebanada',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 pieza o rebanada',
              value: 0.75
            },
            {
              label: '1 pieza o rebanada',
              value: 1
            },
            {
              label: '1 1/2 piezas o rebanadas',
              value: 1.5
            },
            {
              label: '2 piezas o rebanadas',
              value: 2
            },
            {
              label: '3 piezas o rebanadas',
              value: 3
            },
            {
              label: '4 piezas o rebanadas',
              value: 4
            },
            {
              label: '5 piezas o rebanadas',
              value: 5
            },
            {
              label: '6 piezas o rebanadas',
              value: 6
            },
            {
              label: '7 piezas o rebanadas',
              value: 7
            },
            {
              label: '8 piezas o rebanadas',
              value: 8
            },
            {
              label: '9 piezas o rebanadas',
              value: 9
            }
          ]
        },
        {
          id: 6,
          seccion: '',
          numero: 33,
          pregunta: `<span class="text-weight-bold">Galletas dulces, panecillos de fibra, biscotties, alfajores, barras de cereal o galletas grandes tipo Starbucks; 
                    ya sean empaquetados, elaborados en casa a base de harinas preparadas o vendidos en restaurantes o cafeterías. </span>`,
          parteDos: `<span class="text-weight-bold">33a.&nbsp Cuando come alguno de estos productos ¿cuántas porciones consume habitualmente? 
                    Una porción equivale a 6 galletas o panecillos chicos; 2 alfajores, biscotties o barras de cereal o 1 galleta grande</span>`,
          opciones: [
            {
              label: 'Menos de 1 porción',
              value: 0.5
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: 'Más de 1 porción',
              value: 1.5
            }
          ]
        },
        {
          id: 7,
          seccion: '',
          numero: 34,
          pregunta: `<span class="text-weight-bold">Productos de panadería salada empleados para preparar sus alimentos o acompañarlos dentro o fuera de casa, ya sean empaquetados, congelados o de panaderías.</span><br>
                    <span class="text-weight-light">P. ej., bolillo, telera, baguette, pan de caja (blanco o integral), pan tostado, bagel, english muffin, bollos para hamburguesa o hot dogs. <u>No</u> considere los panes incluidos 
                    en las hamburguesas, sándwiches, molletes, etc., que ya reportó consumir como productos preparados en restaurantes u otros establecimientos.</span>`,
          parteDos: `<span class="text-weight-bold">34a.&nbsp Cuando come productos de panadería salada ¿cuántas porciones consume habitualmente? Una porción equivale a 
                    1 pieza de pan, 1/3 de baguette, o 2 rebanadas de pan de caja o tostado</span>`,
          opciones: [
            {
              label: 'Menos de 1 porción',
              value: 0.5
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: 'Más de 1 porción',
              value: 2
            }
          ]
        },
        {
          id: 8,
          seccion: '',
          numero: 35,
          pregunta: `<span class="text-weight-bold">Galletas saladas, pretzels, palitos de pan, crostinis, Melba o galletas para sopa, ya sean empaquetados, de restaurantes o cafeterías.</span>`,
          parteDos: `<span class="text-weight-bold">35a.&nbsp Cuando come algunos de estos productos ¿cuántas porciones consume habitualmente? Una porción equivale a 
                    3 galletas, palitos de pan o pretzels, o 10 galletas para sopa.</span>`,
          opciones: [
            {
              label: 'Menos de 1 porción',
              value: 0.5
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: 'Más de 1 porción',
              value: 2
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
      this.$emit('router', 4)
    },
    previousPage () {
      this.$emit('router', 2)
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
