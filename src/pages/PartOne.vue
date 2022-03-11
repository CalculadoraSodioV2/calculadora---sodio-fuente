<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-headline text-white">
            I. ALIMENTOS PREPARADOS FUERA DE CASA (EN RESTAURANTES, ESTABLECIMIENTOS DE COMIDA RÁPIDA O CAFETERIAS) <br /><br />
            SECCIÓN 1 DE 4
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading text-weight-bold q-mt-md bg-teal-1 q-pa-md">
            Díganos con qué frecuencia consume los siguientes alimentos preparados fuera de casa. Considere también los
            alimentos que compra ya preparados aunque no los consuma en el establecimiento donde se venden, por ejemplo,
            aquellos que lleva para comer en casa o pide a domicilio.
          </div>
          <div v-for="(pregunta, index) in variablesPreguntas" v-bind:key="pregunta.id" class="q-mt-xl">
            <div class="q-headline q-mt-lg text-secondary text-weight-bold" v-if="pregunta.seccion != ''" :id="index">
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
                          v-model="porciones[pregunta.id]"
                          :index=index
                          v-on:scroll="nextQuestion($event + 1)">
              </template-two>
            </q-slide-transition>
          </div>
          <div class="row reverse">
            <q-btn label="Continuar"
                  color="secondary"
                  size="lg"
                  align="right"
                  class="q-mt-xl"
                  @click="nextPage()"/>
          </div>
        </q-card-main>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import templateOne from '../components/template-one.vue'
import templateTwo from '../components/template-two.vue'
var VueScrollTo = require('vue-scrollto')

export default {
  name: 'PartOne',
  data () {
    return {
      variablesPreguntas: [
        {
          id: 0,
          type: 1,
          numero: 1,
          seccion: 'Desayunos',
          pregunta: `<span class="text-weight-bold">Paquetes de desayunos de establecimientos de comida rápida (McDonald’s, Burger King, Carl’s Jr.).</span><br/>
                    <span class="text-weight-light">P. ej., molletes, huevos, burritos, cuernitos rellenos, bisquets rellenos, hot cakes, etc.</span>`,
          parteDos: `<span class="text-weight-bold">1a.&nbsp Cada vez que come alguno de estos desayunos ¿cuántas ordenes, paquetes o porciones individuales consume habitualmente?</span>`,
          opciones: [
            {
              label: `Menos de la mitad de 1 orden o porción`,
              value: 0.25
            },
            {
              label: 'La mitad de 1 orden o porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 orden o porción',
              value: 0.75
            },
            {
              label: '1 orden o porción',
              value: 1
            },
            {
              label: '1 1/2 órdenes o porciones',
              value: 1.5
            },
            {
              label: '2 órdenes o porciones',
              value: 2
            },
            {
              label: '3 órdenes o porciones',
              value: 3
            },
            {
              label: '4 órdenes o porciones',
              value: 4
            },
            {
              label: '5 órdenes o porciones',
              value: 5
            },
            {
              label: '6 órdenes o porciones',
              value: 6
            },
            {
              label: '7 órdenes o porciones',
              value: 7
            },
            {
              label: '8 órdenes o porciones',
              value: 8
            },
            {
              label: '9 órdenes o porciones',
              value: 9
            }
          ]
        },
        {
          id: 1,
          type: 1,
          numero: 2,
          seccion: 'Sándwiches, hamburguesas y pizza',
          pregunta: `<span class="text-weight-bold">Subways, sándwiches, paninis, baguettes, bagels o cuernitos rellenos 
                    (no considere los alimentos que ya reportó en la pregunta anterior de desayuno) en establecimientos de comida rápida, restaurantes 
                    a la carta, tiendas de conveniencia u otros establecimientos tipo cafeterías en su barrio o colonia, a cualquier hora del día (desayuno, comida o cena, etc.).</span>`,
          parteDos: `<span class="text-weight-bold">2a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 pieza',
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
              label: '1 1/2 pieza',
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
          id: 2,
          type: 1,
          numero: 3,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Hamburguesas en establecimientos de comida rápida, restaurantes a la carta u 
                    otros establecimientos tipo cafeterías en su barrio o colonia, a cualquier hora del día (desayuno, comida o cena, etc.).</span><br/>
                    <span class="text-weight-light">P. ej., hamburguesa con o sin queso, de res, de pollo, vegetariana, etc.</span>`,
          parteDos: `<span class="text-weight-bold">3a.&nbsp Cada vez que come hamburguesas ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 pieza',
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
          id: 3,
          type: 1,
          numero: 4,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Pizza de establecimientos de comida rápida, restaurantes a la carta 
                    u otros establecimientos tipo cafeterías en su barrio o colonia, a cualquier hora del día (desayuno, comida o cena, etc.). 
                    También considere las pizzas empaquetadas o congeladas del supermercado o tiendas de conveniencia.</span>`,
          parteDos: `<span class="text-weight-bold">4a.&nbsp Cada vez que come pizza ¿cuántas rebanadas consume habitualmente?</span>`,
          opciones: [
            {
              label: '1 rebanada',
              value: 1
            },
            {
              label: '2 rebanadas',
              value: 2
            },
            {
              label: '3 rebanadas',
              value: 3
            },
            {
              label: '4 rebanadas',
              value: 4
            },
            {
              label: '5 rebanadas',
              value: 5
            },
            {
              label: '6 rebanadas',
              value: 6
            },
            {
              label: '7 rebanadas',
              value: 7
            },
            {
              label: '8 rebanadas',
              value: 8
            },
            {
              label: '9 rebanadas',
              value: 9
            }
          ]
        },
        {
          id: 4,
          type: 1,
          numero: 5,
          seccion: 'Entradas y complementos',
          pregunta: `<span class="text-weight-bold">Papas a la francesa, en gajos, en espiral, hashbrown  o puré de papa, en establecimientos de comida rápida, 
                    restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia (no incluya los alimentos que ya reportó en los desayunos de la pregunta 1).</span>`,
          parteDos: `<span class="text-weight-bold">5a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas porciones individuales consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 porción',
              value: 0.25
            },
            {
              label: 'La mitad de 1 porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 porción',
              value: 0.75
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: '1 1/2 porciones',
              value: 1.5
            },
            {
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
              value: 9
            }
          ]
        },
        {
          id: 5,
          type: 1,
          numero: 6,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Alitas de pollo o palomitas de pollo en 
                    establecimientos de comida rápida, restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia. </span><br/>
                    <span class="text-weight-light">P. ej., alitas con hueso o sin hueso, naturales o con salsa picante, BBQ, buffalo, chipotle, etc. <u>No</u> considere los nuggets.</span>`,
          parteDos: `<span class="text-weight-bold">6a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 2 alitas o menos de 4 palomitas',
              value: 0.5
            },
            {
              label: '2 alitas o 4 palomitas',
              value: 1
            },
            {
              label: '4 alitas u 8 palomitas',
              value: 2
            },
            {
              label: '6 alitas o 12 palomitas',
              value: 3
            },
            {
              label: '8 alitas o 16 palomitas',
              value: 4
            },
            {
              label: '10 alitas o 20 palomitas',
              value: 5
            },
            {
              label: '12 alitas o 24 palomitas',
              value: 6
            }
          ]
        },
        {
          id: 6,
          type: 1,
          numero: 7,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Nuggets o tiras de pollo (empanizadas o crujientes) en 
                    establecimientos de comida rápida, restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia.</span><br/>`,
          parteDos: `<span class="text-weight-bold">7a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 3 nuggets o menos de 1 tira de pollo',
              value: 0.5
            },
            {
              label: '3 nuggets o 1 tira de pollo',
              value: 1
            },
            {
              label: '6 nuggets o 2 tiras de pollo',
              value: 2
            },
            {
              label: '9 nuggets o 3 tiras de pollo',
              value: 3
            },
            {
              label: '12 nuggets o 4 tiras de pollo',
              value: 4
            },
            {
              label: '15 nuggets o 5 tiras de pollo',
              value: 5
            },
            {
              label: '18 nuggets o 6 tiras de pollo',
              value: 6
            }
          ]
        },
        {
          id: 7,
          type: 1,
          numero: 8,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Aros de cebolla o dedos de queso
                     en establecimientos de comida rápida, restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia.</span><br/>`,
          parteDos: `<span class="text-weight-bold">8a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas porciones consume habitualmente?. 
                      Una porción equivale a una orden mediana de aros de cebolla (130 g) o 2 dedos de queso.</span>`,
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
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
              value: 9
            }
          ]
        },
        {
          id: 8,
          type: 1,
          numero: 9,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Pan servido como complemento en sus alimentos, como pan de ajo, pan de queso, pan italiano, 
                    bisquets, en establecimientos de comida rápida, restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia. </span>`,
          parteDos: `<span class="text-weight-bold">9a.&nbsp Cada vez que come alguno de estos panes ¿cuántas piezas consume habitualmente?</span>`,
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
          id: 9,
          type: 1,
          numero: 10,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Otras entradas o complementos en restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia.</span><br/>
                    <span class="text-weight-light">P. ej., guacamole, nachos con queso, calamares fritos, cazuela de queso, sopecitos, taquitos dorados, chistorra, etc. <u>No</u> consideres ensaladas ni sopas.</span>`,
          parteDos: `<span class="text-weight-bold">10a.&nbsp Cada vez que come alguno de estos alimentos ¿cuántas ordenes (como las sirve el restaurante) consume habitualmente?</span>`,
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
        },
        {
          id: 10,
          type: 1,
          numero: 11,
          seccion: 'Sopas y ensaladas',
          pregunta: `<span class="text-weight-bold">Sopas secas o caldosas, consomés y cremas en establecimientos de comida rápida, restaurantes a la carta u otros establecimientos 
                    tipo cafeterías en su barrio o colonia. No considere cocinas económicas o comedores en su lugar de trabajo, ya que estos se preguntarán más adelante. </span><br/>
                    <span class="text-weight-light">P. ej., sopa de tortilla, sopa de codito, sopa caldosa de pasta con pollo, cremas, sopa de verdura, consomé, etc. <u>No</u> considere las pastas que consume como platillo principal.</span>`,
          parteDos: `<span class="text-weight-bold">11a.&nbsp Cada vez que come sopas ¿cuántos platos consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 plato',
              value: 0.25
            },
            {
              label: 'La mitad de 1 plato',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 plato',
              value: 0.75
            },
            {
              label: '1 plato',
              value: 1
            },
            {
              label: '1 1/2 platos',
              value: 1.5
            },
            {
              label: '2 platos',
              value: 2
            },
            {
              label: '3 platos',
              value: 3
            },
            {
              label: '4 platos',
              value: 4
            },
            {
              label: '5 platos',
              value: 5
            },
            {
              label: '6 platos',
              value: 6
            },
            {
              label: '7 platos',
              value: 7
            },
            {
              label: '8 platos',
              value: 8
            },
            {
              label: '9 platos',
              value: 9
            }
          ]
        },
        {
          id: 11,
          type: 1,
          numero: 12,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Ensaladas <u>sin</u> pollo, carne, pescado, embutidos ni mariscos en establecimientos
                     de comida rápida, restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia. <u>No</u> considere
                     cocinas económicas o comedores en su lugar de trabajo, ya que estos se preguntarán más adelante.</span><br/>
                     <span class="text-weight-light">P. ej., ensalada mixta, ensalada verde, ensalada cesar, ensalada de col, ensalada rusa, ensalada verde con frutos rojos, etc.</span>`,
          parteDos: `<span class="text-weight-bold">12a.&nbsp Cada vez que come ensalada ¿cuántas porciones individuales (como las sirve el restaurante) consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 porción',
              value: 0.25
            },
            {
              label: 'La mitad de 1 porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 porción',
              value: 0.75
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: '1 1/2 porciones',
              value: 1.5
            },
            {
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
              value: 9
            }
          ]
        },
        {
          id: 12,
          type: 1,
          numero: 13,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Ensaladas que contengan pollo, carne, pescado, 
                    embutidos o mariscos en establecimientos de comida rápida, restaurantes a la carta u otros establecimientos
                     tipo cafeterías en su barrio o colonia. <u>No</u> considere cocinas económicas o comedores en su lugar de trabajo, 
                     ya que estos se preguntarán más adelante.</span><br/>
                     <span class="text-weight-light">P. ej., ensalada cesar con pollo, ensalada con pollo a la parrilla, ensalada con pollo crujiente, ensalada del chef, ensalada con camarones, etc.</span>`,
          parteDos: `<span class="text-weight-bold">13a.&nbsp Cada vez que come ensalada ¿cuántas porciones individuales (como las sirve el restaurante) consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 porción',
              value: 0.25
            },
            {
              label: 'La mitad de 1 porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 porción',
              value: 0.75
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: '1 1/2 porciones',
              value: 1.5
            },
            {
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
              value: 9
            }
          ]
        },
        {
          id: 13,
          type: 1,
          numero: 14,
          seccion: 'Platillos mixtos',
          pregunta: `<span class="text-weight-bold">Pollo frito en establecimientos de comida rápida (tipo KFC).`,
          parteDos: `<span class="text-weight-bold">14a.&nbsp Cada vez que come pollo frito ¿cuántas piezas consume habitualmente?</span>`,
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
          id: 14,
          type: 1,
          numero: 15,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Pollo rostizado de rosticerías, supermercados o algún otro establecimientos en 
                    su barrio o colonia. <u>No</u> considere cocinas económicas o comedores en su lugar de trabajo, ya que estos se preguntarán más adelante.`,
          parteDos: `<span class="text-weight-bold">15a.&nbsp Cada vez que come pollo rostizado ¿cuántas piezas consume habitualmente?</span>`,
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
          id: 15,
          type: 1,
          numero: 16,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Platillos a base de pasta como espagueti, ravioles, fettuccine, lasaña, etc., en cualquier 
                  tipo de salsa o crema, <u>con o sin</u> carne, pescado, mariscos, embutidos o pollo, en establecimientos de comida rápida, 
                  restaurantes a la carta u otros establecimientos tipo cafeterías en su barrio o colonia. No considere cocinas económicas 
                  o comedores en su lugar de trabajo, ya que estos se preguntarán más adelante.</span><br/>
                    <span class="text-weight-light">P. ej., espagueti a la boloñesa, fettuccine Alfredo, lasaña, ravioles rellenos en alguna salsa, pasta con pollo o 
                    camarones, etc. <u>No</u> considere las pastas secas incluidas en la sección de sopas.</span> `,
          parteDos: `<span class="text-weight-bold">16a.&nbsp Cada vez que come un platillo a base de pasta ¿cuántas porciones individuales (como las sirve el restaurante) consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 porción',
              value: 0.25
            },
            {
              label: 'La mitad de 1 porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 porción',
              value: 0.75
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: '1 1/2 porciones',
              value: 1.5
            },
            {
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
              value: 9
            }
          ]
        },
        {
          id: 16,
          type: 1,
          numero: 17,
          seccion: '',
          pregunta: `<span class="text-weight-bold">Platillos a base de carne, pollo, pescado o mariscos en restaurantes a la carta u otros 
                    establecimientos tipo cafeterías en su barrio o colonia. <u>No</u> considere cocinas económicas o comedores en su lugar de trabajo,
                     ya que estos se preguntarán más adelante. <u>No</u> incluya ensaladas o pastas que contengan carne, pescado, mariscos o 
                     pollo porque estas ya se preguntaron previamente.</span>`,
          parteDos: `<span class="text-weight-bold">17a.&nbsp Cada vez que come un platillo a base de carne, pollo, pescado o mariscos ¿cuántas 
                    porciones individuales (como las sirve el restaurante) come habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de la mitad de 1 porción',
              value: 0.25
            },
            {
              label: 'La mitad de 1 porción',
              value: 0.5
            },
            {
              label: 'Poco más de la mitad de 1 porción',
              value: 0.75
            },
            {
              label: '1 porción',
              value: 1
            },
            {
              label: '1 1/2 porciones',
              value: 1.5
            },
            {
              label: '2 porciones',
              value: 2
            },
            {
              label: '3 porciones',
              value: 3
            },
            {
              label: '4 porciones',
              value: 4
            },
            {
              label: '5 porciones',
              value: 5
            },
            {
              label: '6 porciones',
              value: 6
            },
            {
              label: '7 porciones',
              value: 7
            },
            {
              label: '8 porciones',
              value: 8
            },
            {
              label: '9 porciones',
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
      this.$emit('router', 2)
    },
    consoles () {
      console.log(this.porciones)
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
      for (let i = 0; i < 17; i++) {
        this.preguntas[i] = '1'
        this.returnToZero[i] = false
      }
    },
    nextQuestion (index) {
      VueScrollTo.scrollTo(index)
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
