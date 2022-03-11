<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-headline text-white">
            IV. OTROS ALIMENTOS PROCESADOS O EMPAQUETADOS <br /><br />
            SECCIÓN 4 DE 4
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading text-weight-bold q-mt-md bg-teal-1 q-pa-md">
            Díganos con qué frecuencia consume los siguientes productos que compra en supermercados, tiendas de conveniencia o tiendas en su barrio o colonia,
            y que usa en casa. No considere los ingredientes o alimentos que vienen incluidos en las comidas preparadas que compra en restaurantes, cafeterías,
            cocinas económicas o que consume en el comedor de su lugar de trabajo.
            Por ejemplo, sí cuente el jamón que usó para preparar un sándwich en casa, pero no considere el contenido de un sándwich que compró en una cafetería.
          </div>

          <div v-for="pregunta in variablesPreguntas" v-bind:key="pregunta.id" class="q-mt-xl">
            <div class="q-headline q-mt-lg text-secondary text-weight-bold" v-if="pregunta.seccion != ''">
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

          <div class="q-mt-xl">
            <div class="q-headline q-mt-lg text-secondary text-weight-bold">
              {{ pregunta71.seccion }}
            </div>

            <template-two-slider
                          :questionTwo=pregunta71.parteUno
                          :label=pregunta71.opciones1
                          :ret=returnToZero70
                          v-model="preguntas[35]">
            </template-two-slider>

            <q-slide-transition>
              <template-two-slider v-show="preguntas[35] != 0"
                          :questionTwo=pregunta71.parteDos
                          :label=pregunta71.opciones2
                          :ret=false
                          v-model="porciones[35]">
              </template-two-slider>
            </q-slide-transition>
          </div>

          <div class="q-mt-xl">
            <template-two-slider
                          :questionTwo=pregunta72.parteUno
                          :label=pregunta72.opciones
                          :ret=false
                          v-model="preguntas[36]">
            </template-two-slider>
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
import templateTwoSlider from '../components/template-two-slider.vue'

export default {
  name: 'PartFour',
  data () {
    return {
      variablesPreguntas: [
        {
          id: 0,
          seccion: 'Verduras y legumbres',
          numero: 36,
          pregunta: `<span class="text-weight-bold">Encurtidos como aceitunas, alcaparras, pepinillos, cebollitas o elotitos. </span>`,
          parteDos: `<span class="text-weight-bold">36a.&nbsp Cuando come estos productos encurtidos ¿cuántas porciones consume habitualmente? 
                    Una porción equivale a 1 aceituna, cebollita, elotito, 1 rebanada de pepinillo, o 1 cucharadita de alcaparras</span>`,
          opciones: [
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
          id: 1,
          seccion: '',
          numero: 37,
          pregunta: `<span class="text-weight-bold">Verduras en salmuera envasadas o sazonadas congeladas. </span>`,
          parteDos: `<span class="text-weight-bold">37a.&nbsp Cuando come este tipo de verduras ¿cuánto consume habitualmente?</span>`,
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
          id: 2,
          seccion: '',
          numero: 38,
          pregunta: `<span class="text-weight-bold">Chiles en conserva (en escabeche o adobados) </span>`,
          parteDos: `<span class="text-weight-bold">38a.&nbsp Cuando come chiles en conserva ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1/4 taza',
              value: 0.5
            },
            {
              label: '1/4 de taza',
              value: 1
            },
            {
              label: '1/2 taza',
              value: 2
            },
            {
              label: '3/4 taza',
              value: 3
            },
            {
              label: '1 taza',
              value: 4
            }
          ]
        },
        {
          id: 3,
          seccion: '',
          numero: 39,
          pregunta: `<span class="text-weight-bold">Frijoles enteros o refritos empaquetados, en lata o bolsa.</span>`,
          parteDos: `<span class="text-weight-bold">39a.&nbsp Cuando come frijoles empaquetados ¿cuánto consume habitualmente?</span>`,
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
          numero: 40,
          pregunta: `<span class="text-weight-bold">Puré de papa sazonado o saborizado, empaquetado o preparado en casa a partir de hojuelas o polvo.</span>`,
          parteDos: `<span class="text-weight-bold">40a.&nbsp Cuando come este tipo de puré de papa ¿cuánto consume habitualmente?</span>`,
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
              label: '3/4 taza',
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
          id: 5,
          seccion: '',
          numero: 41,
          pregunta: `<span class="text-weight-bold">Jugos de tomate o de verduras para beber, ya sea natural, con jugo de almeja o sazonado, envasado en lata, bote o tetra brik.</span>`,
          parteDos: `<span class="text-weight-bold">41a.&nbsp Cuando toma estos jugos procesados ¿cuántos vasos bebe habitualmente? Un vaso equivale a 240 ml</span>`,
          opciones: [
            {
              label: 'Menos de 1 vaso',
              value: 0.5
            },
            {
              label: '1 vaso',
              value: 1
            },
            {
              label: '1 1/2 vasos',
              value: 1.5
            },
            {
              label: '2 vasos',
              value: 4
            },
            {
              label: '3 vasos',
              value: 6
            },
            {
              label: '4 vasos',
              value: 8
            },
            {
              label: '5 vasos',
              value: 10
            },
            {
              label: '6 vasos',
              value: 12
            },
            {
              label: '7 vasos',
              value: 14
            },
            {
              label: '8 vasos',
              value: 16
            },
            {
              label: '9 vasos',
              value: 18
            }
          ]
        },
        {
          id: 6,
          seccion: 'Leche y derivados',
          numero: 42,
          pregunta: `<span class="text-weight-bold">Leche natural o saborizada, yogurt, leche vegetal (soya, almendra, arroz o coco) o bebidas de café (latte, cappuccino o frappuccino) 
                    envasadas o preparadas a partir de polvos. </span>`,
          parteDos: `<span class="text-weight-bold">42a.&nbsp Cuando toma leche de vaca o vegetal, o alguna de estas bebidas envasadas ¿cuántos vasos bebe habitualmente? 
                    Un vaso equivale a 240 ml</span>`,
          opciones: [
            {
              label: 'Menos de 1/2 vaso',
              value: 0.25
            },
            {
              label: '1/2 vaso',
              value: 0.5
            },
            {
              label: 'Poco más de 1/2 vaso',
              value: 0.75
            },
            {
              label: '1 vaso',
              value: 1
            },
            {
              label: '1 1/2 vasos',
              value: 1.5
            },
            {
              label: '2 vasos',
              value: 2
            },
            {
              label: '3 vasos',
              value: 3
            },
            {
              label: '4 vasos',
              value: 4
            },
            {
              label: '5 vasos',
              value: 5
            },
            {
              label: '6 vasos',
              value: 6
            },
            {
              label: '7 vasos',
              value: 7
            },
            {
              label: '8 vasos',
              value: 8
            },
            {
              label: '9 vasos',
              value: 9
            }
          ]
        },
        {
          id: 7,
          seccion: '',
          numero: 43,
          pregunta: `<span class="text-weight-bold">Consumo de queso cottage.`,
          parteDos: `<span class="text-weight-bold">43a.&nbsp Cuando come este tipo de queso ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 8,
          seccion: '',
          numero: 44,
          pregunta: `<span class="text-weight-bold">Queso fresco, panela, ranchero, requesón, ricotta, oaxaca, mozzarella, asadero o adobera. </span>`,
          parteDos: `<span class="text-weight-bold">44a.&nbsp Cuando come alguno de estos quesos ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 rebanada o cucharada',
              value: 0.5
            },
            {
              label: '1 rebanada o cucharada',
              value: 1
            },
            {
              label: '2 rebanadas o cucharadas',
              value: 2
            },
            {
              label: '3 rebanadas o cucharadas',
              value: 3
            },
            {
              label: '4 rebanadas o cucharadas',
              value: 4
            },
            {
              label: '5 rebanadas o cucharadas',
              value: 5
            },
            {
              label: '6 rebanadas o cucharadas',
              value: 6
            },
            {
              label: '7 rebanadas o cucharadas',
              value: 7
            },
            {
              label: '8 rebanadas o cucharadas',
              value: 8
            },
            {
              label: '9 rebanadas o cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 9,
          seccion: '',
          numero: 45,
          pregunta: `<span class="text-weight-bold">Queso crema para untar (natural o saborizado), ya sea para cocinar o adicionar a los alimentos.</span>`,
          parteDos: `<span class="text-weight-bold">45a.&nbsp Cuando come este tipo de queso ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 10,
          seccion: '',
          numero: 46,
          pregunta: `<span class="text-weight-bold">Queso fundido en rebanadas (p.ej., queso amarillo), líquido (tipo para nachos) o para untar (p. ej., Cheez Whiz) 
                    que <u>usa solo en su casa</u> para preparar sus alimentos.</span>`,
          parteDos: `<span class="text-weight-bold">46a.&nbsp Cuando come alguno de estos quesos procesados ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 rebanada o cucharada',
              value: 0.5
            },
            {
              label: '1 rebanada o cucharada',
              value: 1
            },
            {
              label: '2 rebanadas o cucharadas',
              value: 2
            },
            {
              label: '3 rebanadas o cucharadas',
              value: 3
            },
            {
              label: '4 rebanadas o cucharadas',
              value: 4
            },
            {
              label: '5 rebanadas o cucharadas',
              value: 5
            },
            {
              label: '6 rebanadas o cucharadas',
              value: 6
            },
            {
              label: '7 rebanadas o cucharadas',
              value: 7
            },
            {
              label: '8 rebanadas o cucharadas',
              value: 8
            },
            {
              label: '9 rebanadas o cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 11,
          seccion: '',
          numero: 47,
          pregunta: `<span class="text-weight-bold">Consumo de otros quesos. </span><br>
                    <span class="text-weight-light">P.ej., manchego, chihuahua, parmesano, romano, feta, de cabra, gouda, cheddar, edam, havarti, camembert, brie, etc.</span>`,
          parteDos: `<span class="text-weight-bold">47a.&nbsp Cuando come alguno de estos quesos ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 rebanada o cucharada',
              value: 0.5
            },
            {
              label: '1 rebanada o cucharada',
              value: 1
            },
            {
              label: '2 rebanadas o cucharadas',
              value: 2
            },
            {
              label: '3 rebanadas o cucharadas',
              value: 3
            },
            {
              label: '4 rebanadas o cucharadas',
              value: 4
            },
            {
              label: '5 rebanadas o cucharadas',
              value: 5
            },
            {
              label: '6 rebanadas o cucharadas',
              value: 6
            },
            {
              label: '7 rebanadas o cucharadas',
              value: 7
            },
            {
              label: '8 rebanadas o cucharadas',
              value: 8
            },
            {
              label: '9 rebanadas o cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 12,
          seccion: 'Aceites y grasas',
          numero: 48,
          pregunta: `<span class="text-weight-bold">Aderezos para ensalada, vinagretas, mayonesa, chimichurri, hummus o dips. <u>No</u> considere preparaciones caseras <u>sin sal añadida</u> 
                    (p. ej., vinagreta a base de aceite de oliva y vinagre sin sal).</span>`,
          parteDos: `<span class="text-weight-bold">48a.&nbsp Cuando come aderezos para ensalada, mayonesa, chimichurri, hummus o dips ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 13,
          seccion: '',
          numero: 49,
          pregunta: `<span class="text-weight-bold">Mantequilla o margarina con sal para cocinar o adicionada a los alimentos. <u>No</u> incluya la mantequilla o margarina que utiliza para preparar productos de repostería.</span>`,
          parteDos: `<span class="text-weight-bold">49a.&nbsp Cuando come mantequilla o margarina ¿cuánto consume habitualmente? En caso de que el alimento preparado rinda varias porciones, 
                    indique solo la cantidad contenida en la porción que usted consume.</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 14,
          seccion: '',
          numero: 50,
          pregunta: `<span class="text-weight-bold">Tocino, chorizo para freír (cerdo, pollo, pavo o soya), longaniza, paté (cerdo, res, pavo, ternera o atún) o jamón del diablo.</span>`,
          parteDos: `<span class="text-weight-bold">50a.&nbsp Cuando come estos embutidos ¿cuántas porciones consume habitualmente? Una porción equivale a 15g (1 
                    cucharada) de chorizo, longaniza o paté, o 1 rebanada de tocino. Considere la cantidad de tocino, chorizo y longaniza una vez fritos. </span>`,
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
          id: 15,
          seccion: 'Cereales y derivados',
          numero: 51,
          pregunta: `<span class="text-weight-bold">Cereal de caja (cereales de desayuno) o avena instantánea saborizada.</span>`,
          parteDos: `<span class="text-weight-bold">51a.&nbsp Cuando come este tipo de cereales ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 3/4 de taza o menos de una cajita individual',
              value: 0.5
            },
            {
              label: '3/4 a 1 taza o 1 cajita individual',
              value: 1
            },
            {
              label: '2 tazas o 2 cajitas individuales',
              value: 2
            },
            {
              label: '3 tazas o 3 cajitas individuales',
              value: 3
            },
            {
              label: '4 tazas o 4 cajitas individuales',
              value: 4
            },
            {
              label: '5 tazas o 5 cajitas individuales',
              value: 5
            },
            {
              label: '6 tazas o 6 cajitas individuales',
              value: 6
            },
            {
              label: '7 tazas o 7 cajitas individuales',
              value: 7
            },
            {
              label: '8 tazas o 8 cajitas individuales',
              value: 8
            },
            {
              label: '9 tazas o 9 cajitas individuales',
              value: 9
            }
          ]
        },
        {
          id: 16,
          seccion: '',
          numero: 52,
          pregunta: `<span class="text-weight-bold">Hot cakes o waffles empaquetados, congelados o elaborados en casa a base de harinas preparadas.</span>`,
          parteDos: `<span class="text-weight-bold">52a.&nbsp Cuando come alguno de estos productos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 pieza',
              value: 0.5
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
          id: 17,
          seccion: '',
          numero: 53,
          pregunta: `<span class="text-weight-bold">Pan árabe, tortillas de harina o crepas empaquetadas, congeladas o elaboradas a base de harinas preparadas.</span>`,
          parteDos: `<span class="text-weight-bold">53a.&nbsp Cuando come alguno de estos productos ¿cuántas piezas consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 pieza',
              value: 0.5
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
          id: 18,
          seccion: '',
          numero: 54,
          pregunta: `<span class="text-weight-bold">Pasta seca o arroz sazonados, ya sean empaquetados para preparar, instantáneos, listos para servir o congelados. 
                    <u>No</u> incluya sopas aguadas de pasta, ya que éstas se preguntarán más adelante.</span>`,
          parteDos: `<span class="text-weight-bold">54a.&nbsp Cuando come este tipo de platillos ¿cuánto consume habitualmente del producto ya preparado?</span>`,
          opciones: [
            {
              label: 'Menos de 1 taza o paquete individual',
              value: 0.5
            },
            {
              label: '1 taza o paquete individual',
              value: 1
            },
            {
              label: '2 tazas o paquetes individuales',
              value: 2
            },
            {
              label: '3 tazas o paquetes individuales',
              value: 3
            },
            {
              label: '4 tazas o paquetes individuales',
              value: 4
            },
            {
              label: '5 tazas o paquetes individuales',
              value: 5
            },
            {
              label: '6 tazas o paquetes individuales',
              value: 6
            },
            {
              label: '7 tazas o paquetes individuales',
              value: 7
            },
            {
              label: '8 tazas o paquetes individuales',
              value: 8
            },
            {
              label: '9 tazas o paquetes individuales',
              value: 9
            }
          ]
        },
        {
          id: 19,
          seccion: 'Sopas, caldos, salsas y condimentos',
          numero: 55,
          pregunta: `<span class="text-weight-bold">Sopas caldosas a base de pastas sazonadas instantáneas; cremas y sopas condensadas o listas para servir; o caldos y consomés 
                    (tipo caldos Knorr) preparados a base de polvos, cubos o listos para servir.</span>`,
          parteDos: `<span class="text-weight-bold">55a.&nbsp Cuando come este tipo de sopas, cremas o caldos ¿cuánto consume habitualmente del producto ya preparado?</span>`,
          opciones: [
            {
              label: 'Menos de 1 taza o paquete',
              value: 0.5
            },
            {
              label: '1 taza o paquete',
              value: 1
            },
            {
              label: '2 tazas o paquetes',
              value: 2
            },
            {
              label: '3 tazas o paquetes',
              value: 3
            },
            {
              label: '4 tazas o paquetes',
              value: 4
            },
            {
              label: '5 tazas o paquetes',
              value: 5
            },
            {
              label: '6 tazas o paquetes',
              value: 6
            },
            {
              label: '7 tazas o paquetes',
              value: 7
            },
            {
              label: '8 tazas o paquetes',
              value: 8
            },
            {
              label: '9 tazas o paquetes',
              value: 9
            }
          ]
        },
        {
          id: 20,
          seccion: '',
          numero: 56,
          pregunta: `<span class="text-weight-bold">Salsas empaquetadas para marinar carne, tipo BBQ, gravy, moles, adobos y caldillos para guisados, ya sean listos para servirse, condensados o en pasta.</span>`,
          parteDos: `<span class="text-weight-bold">56a.&nbsp Cuando come este tipo de productos ¿cuánto consume habitualmente del producto ya preparado?</span>`,
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
          id: 21,
          seccion: '',
          numero: 57,
          pregunta: `<span class="text-weight-bold">Puré de tomate condimentado o salsas para pasta a base de quesos, tomate o pesto.</span><br/>
                    <span class="text-weight-light">P. ej., salsa de quesos, salsa Alfredo, salsa de tomate con champiñones, salsa de tomate con carne bolognesa, etc.</span>`,
          parteDos: `<span class="text-weight-bold">57a.&nbsp Cuando come este tipo de puré o salsas para pastas ¿cuánto consume habitualmente?</span>`,
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
          id: 22,
          seccion: '',
          numero: 58,
          pregunta: `<span class="text-weight-bold">Salsas picantes, botaneras, chamoy líquido y salsas envasadas tipo casera.</span><br/>
                    <span class="text-weight-light">P. ej., salsas Tabasco, Tajín líquido, Valentina, Buffalo, Botanera, chamoy líquido, salsa envasada tipo casera verde, roja, de chipotle, guacamole, etc.`,
          parteDos: `<span class="text-weight-bold">58a.&nbsp Cuando come este tipo de salsas ¿cuánto consume habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 23,
          seccion: '',
          numero: 59,
          pregunta: `<span class="text-weight-bold">Salsas y jugos sazonadores, mezclas para micheladas, salsa de soya y otras salsas orientales (teriyaki, hoisin, etc.), 
                    ya sea para cocinar o adicionar a sus alimentos o bebidas. </span>`,
          parteDos: `<span class="text-weight-bold">59a.&nbsp Cuando come este tipo de salsas ¿cuánto come habitualmente? En caso de que el alimento o 
                    bebida preparada rinda varias porciones, indique solo la cantidad contenida en la porción que usted consume.</span>`,
          opciones: [
            {
              label: 'Menos de 1 cucharada',
              value: 0.5
            },
            {
              label: '1 cucharada',
              value: 1
            },
            {
              label: '2 cucharadas',
              value: 2
            },
            {
              label: '3 cucharadas',
              value: 3
            },
            {
              label: '4 cucharadas',
              value: 4
            },
            {
              label: '5 cucharadas',
              value: 5
            },
            {
              label: '6 cucharadas',
              value: 6
            },
            {
              label: '7 cucharadas',
              value: 7
            },
            {
              label: '8 cucharadas',
              value: 8
            },
            {
              label: '9 cucharadas',
              value: 9
            }
          ]
        },
        {
          id: 24,
          seccion: '',
          numero: 60,
          pregunta: `<span class="text-weight-bold">Condimentos, sazonadores con sal y consomés de pollo, ya sea para cocinar o adicionados a sus platillos.</span><br/>
                    <span class="text-weight-light">P. ej., sal con cebolla o ajo, sazonadores para carnes o mariscos, consomé de pollo en polvo, ablandadores de carne, chile en polvo con sal, 
                    hojas sazonadoras, sazonadores para arroz, etc.</span>`,
          parteDos: `<span class="text-weight-bold">60a.&nbsp Cuando come este tipo de condimentos o sazonadores ¿cuánto come habitualmente? 
                    En caso de que el alimento preparado sea para varias personas, indique solo la cantidad contenida en la porción que usted come.</span>`,
          opciones: [
            {
              label: 'Menos de ½ cucharadita o menos de 1 hoja sazonadora',
              value: 0.5
            },
            {
              label: '1/2 cucharadita o 1 hoja sazonadora',
              value: 1
            },
            {
              label: '1 cucharadita o 2 hojas sazonadoras',
              value: 2
            },
            {
              label: '1 1/2 cucharaditas o 3 hojas sazonadoras',
              value: 3
            },
            {
              label: '2 cucharaditas o 4 hojas sazonadoras ',
              value: 4
            }
          ]
        },
        {
          id: 25,
          seccion: 'Carnes, pescados, mariscos y sustitutos',
          numero: 61,
          pregunta: `<span class="text-weight-bold">Carne de res (sola o mezclada con soya) o de cerdo, sazonadas o marinadas, ya sean empaquetadas, congeladas o compradas en carnicerías.</span><br/>
                    <span class="text-weight-light">P. ej., arrachera, cecina, cecina enchilada, fajitas de res marinadas o de res con soya marinadas, carne para hamburguesa de res o de res con soya, 
                    carne al pastor, carne seca (machaca), etc.</span>`,
          parteDos: `<span class="text-weight-bold">61a.&nbsp Cuando come carne de res o de cerdo sazonada o marinada ¿cuántas porciones consume habitualmente? Una porción puede ser: 1 
                    carne para hamburguesa, 120 g de carne sazonada o marinada, o 50 g de carne seca.</span>`,
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
          id: 26,
          seccion: '',
          numero: 62,
          pregunta: `<span class="text-weight-bold">Pollo o pavo preparado, ahumado, sazonado o marinado, empaquetado o congelado.</span><br/>
                    <span class="text-weight-light">P. ej., filete de pechuga marinado, empanizado o relleno, pollo deshebrado sazonado, nuggets, hamburguesas de pollo o pavo, alitas, boneless, fajitas, etc.</span>`,
          parteDos: `<span class="text-weight-bold">62a.&nbsp Cuando come pollo o pavo preparado, ahumado, sazonado o marinado ¿cuántas porciones consume habitualmente? Una porción puede ser: 1 hamburguesa, 
                    1 filete, 120 g de pollo o pavo, 5 nuggets o 3 alitas</span>`,
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
          id: 27,
          seccion: '',
          numero: 63,
          pregunta: `<span class="text-weight-bold">Pescados y mariscos sazonados, marinados, empanizados o ahumados, ya sean empaquetados, congelados o enlatados. Incluya surimi.</span><br/>
                    <span class="text-weight-light">P. ej., filete empanizado o marinado, camarones empanizados o sazonados, barritas de pescado, nuggets, atún en lata o empaquetado, 
                    sardina enlatada en jitomate o aceite, ostiones ahumados, mejillones al ajillo, calamar en su tinta, angulas de surimi al ajillo, etc.</span>`,
          parteDos: `<span class="text-weight-bold">63a.&nbsp Cuando come pescados, mariscos o surimi empaquetados, enlatados o congelados sazonados ¿cuántas porciones 
                    consume habitualmente? Una porción puede ser: 120 g o ½  taza de productos de mar o 5 nuggets.</span>`,
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
          id: 28,
          seccion: '',
          numero: 64,
          pregunta: `<span class="text-weight-bold">Huevo o claras de huevo fresco o empaquetado, cocinados en casa. No incluya el huevo que utiliza para preparar productos de panadería o repostería.</span><br/>`,
          parteDos: `<span class="text-weight-bold">64a.&nbsp Cuando come huevo ¿cuántas piezas come habitualmente?</span>`,
          opciones: [
            {
              label: '1 huevo o 2 claras',
              value: 1
            },
            {
              label: '2 huevos o 4 claras',
              value: 2
            },
            {
              label: '3 huevos o 6 claras',
              value: 3
            },
            {
              label: '4 huevos u 8 claras',
              value: 4
            },
            {
              label: '5 huevos o 10 claras',
              value: 5
            },
            {
              label: '6 huevos o 12 claras',
              value: 6
            }
          ]
        },
        {
          id: 29,
          seccion: '',
          numero: 65,
          pregunta: `<span class="text-weight-bold">Jamón, salchicha o carnes frías. </span><br/>
                    <span class="text-weight-light">P. ej., jamón de pavo o cerdo, salchichas de pavo o cerdo, salchicha cocktail, chorizo tipo español, salami, pepperoni, lomo embuchado, jamón serrano, etc.</span>`,
          parteDos: `<span class="text-weight-bold">65a.&nbsp Cuando come alguna de estas carnes frías ¿cuántas porciones consume habitualmente? Una porción equivale a 3 rebanadas de jamón; 
                    1 salchicha; 5 salchichas cocktail; 6 rebanadas de pepperoni, chorizo, salami o lomo embuchado; o 2 rebanadas de jamón serrano</span>`,
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
          id: 30,
          seccion: '',
          numero: 66,
          pregunta: `<span class="text-weight-bold">Salchicha para asar, chorizo para asar o chistorra.</span><br/>
                    <span class="text-weight-light">P. ej., salchicha de cerdo o pavo para asar, chorizo tipo español o argentino para asar, chorizo parrillero, chorizo a la sidra, chorizo de pavo para asar, etc.</span>`,
          parteDos: `<span class="text-weight-bold">66a.&nbsp Cuando come alguno de estos embutidos ¿cuántas porciones consume habitualmente? Una porción equivale a 1 salchicha o chorizo para asar, o 100 g de chistorra.</span>`,
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
            }
          ]
        },
        {
          id: 31,
          seccion: 'Frituras, botanas y dulces salados o enchilados',
          numero: 67,
          pregunta: `<span class="text-weight-bold">Palomitas de microondas o frituras de maíz, trigo, papa, plátano, nopal u otros vegetales, ya sean sazonadas, saladas o enchiladas. </span><br/>
                    <span class="text-weight-light">P. ej., palomitas de microondas de cualquier sabor, papas fritas, churritos de harina de trigo o de nopal, chicharrones de harina de trigo, botanas de totopos de maíz, platanitos fritos o deshidratados, botanas de harina de papa y otros vegetales como camote, yuca o espinaca; sazonados, salados o enchilados, etc.</span>`,
          parteDos: `<span class="text-weight-bold">67a.&nbsp Cuando come este tipo de frituras ¿cuántas porciones consume habitualmente? Una porción equivale a 1 bolsa estándar de palomitas de microondas o 1 bolsa individual de frituras.</span>`,
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
            }
          ]
        },
        {
          id: 32,
          seccion: '',
          numero: 68,
          pregunta: `<span class="text-weight-bold">Botanas sazonadas, saladas o enchiladas.</span><br/>
                    <span class="text-weight-light">P. ej., cacahuates, nueces, almendras, pistaches, habas, semillas o frutas secas.</span>`,
          parteDos: `<span class="text-weight-bold">68a.&nbsp Cuando come este tipo de botanas ¿cuánto come habitualmente?</span>`,
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
              label: '6 taza',
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
          id: 33,
          seccion: '',
          numero: 69,
          pregunta: `<span class="text-weight-bold">Chicharrón de cerdo duro empaquetado o sin empaquetar, del supermercado o algún establecimiento como carnicerías o mercados.</span><br/>`,
          parteDos: `<span class="text-weight-bold">69a.&nbsp Cuando come chicharrón duro de cerdo ¿cuánto come habitualmente?</span>`,
          opciones: [
            {
              label: 'Menos de 50 g',
              value: 0.5
            },
            {
              label: '50 g',
              value: 1
            },
            {
              label: '100 g',
              value: 2
            },
            {
              label: '150 g',
              value: 3
            },
            {
              label: '200 g',
              value: 4
            },
            {
              label: '250 g',
              value: 5
            },
            {
              label: '300 g',
              value: 6
            },
            {
              label: '350 g',
              value: 7
            },
            {
              label: '400 g',
              value: 8
            },
            {
              label: '450 g',
              value: 9
            },
            {
              label: '500 g',
              value: 10
            }
          ]
        },
        {
          id: 34,
          seccion: '',
          numero: 70,
          pregunta: `<span class="text-weight-bold">Paletas de hielo con chamoy o chile y dulces enchilados.</span><br/>
                    <span class="text-weight-light">P. ej., paletas heladas de mango, tamarindo, piña, etc., con chile o chamoy; paletas de caramelo con chile, dulces de tamarindo con chile o chamoy, gomitas enchiladas, etc.</span>`,
          parteDos: `<span class="text-weight-bold">70a.&nbsp Cuando come paletas heladas o dulces enchilados ¿cuántas porciones consume habitualmente? Una porción equivale a 1 pieza o 3 gomitas o dulces pequeños.</span>`,
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
            }
          ]
        }
      ],
      pregunta71: {
        seccion: `Uso de sal de mesa`,
        parteUno: `<span class="text-weight-bold"><ol><li value='71'>¿Cuántos días a la semana cocina? <br/></li></ol></span>`,
        parteDos: `<span class="text-weight-bold">71a.&nbsp En un día habitual en los que usted cocina ¿qué cantidad de sal 
                    usa en total para preparar sus alimentos de todo el día? En caso de que sea una preparación para toda la familia, 
                    indique solo la cantidad de sal contenida en <u>sus alimentos.</u><br/></span>`,
        opciones1: [
          {
            label: '0 días',
            value: 0
          },
          {
            label: '1 día',
            value: 1
          },
          {
            label: '2 días',
            value: 2
          },
          {
            label: '3 días',
            value: 3
          },
          {
            label: '4 días',
            value: 4
          },
          {
            label: '5 días',
            value: 5
          },
          {
            label: '6 días',
            value: 6
          },
          {
            label: '7 días',
            value: 7
          }
        ],
        opciones2: [
          {
            label: 'No uso sal',
            value: 0
          },
          {
            label: '1/4 cucharadita',
            value: 500
          },
          {
            label: '1/2 cucharadita',
            value: 1000
          },
          {
            label: '1 cucharadita',
            value: 2000
          },
          {
            label: '1 1/2 cucharaditas',
            value: 3000
          },
          {
            label: '2 cucharaditas',
            value: 4000
          }
        ]
      },
      pregunta72: {
        parteUno: `<span class="text-weight-bold">72.&nbsp
                    En un día habitual ¿qué cantidad de sal agrega en la mesa a sus alimentos, 
                    sin importar si come en casa, restaurantes o algún otro establecimiento?.       
                    </span>`,
        opciones: [
          {
            label: '0 sacudidas',
            value: 0
          },
          {
            label: '1 sacudida',
            value: 1
          },
          {
            label: '2 sacudidas',
            value: 2
          },
          {
            label: '3 sacudidas',
            value: 3
          },
          {
            label: '4 sacudidas',
            value: 4
          },
          {
            label: '5 sacudidas',
            value: 5
          },
          {
            label: '6 sacudidas',
            value: 6
          },
          {
            label: '7 sacudidas',
            value: 7
          },
          {
            label: '8 sacudidas',
            value: 8
          },
          {
            label: '9 sacudidas',
            value: 9
          },
          {
            label: '10 sacudidas',
            value: 10
          },
          {
            label: '11 sacudidas',
            value: 11
          },
          {
            label: '12 sacudidas',
            value: 12
          },
          {
            label: '13 sacudidas',
            value: 13
          },
          {
            label: '14 sacudidas',
            value: 14
          },
          {
            label: '15 sacudidas',
            value: 15
          },
          {
            label: '16 sacudidas',
            value: 16
          },
          {
            label: '17 sacudidas',
            value: 17
          },
          {
            label: '18 sacudidas',
            value: 18
          },
          {
            label: '19 sacudidas',
            value: 19
          },
          {
            label: '20 sacudidas',
            value: 20
          }
        ]
      },
      preguntas: [],
      porciones: [],
      respuestas: [],
      returnToZero: [],
      returnToZero70: false
    }
  },
  methods: {
    nextPage () {
      this.$emit('preguntas', this.respuestas)
      this.$emit('calculate', true)
      this.$emit('router', 5)
    },
    previousPage () {
      this.$emit('router', 3)
    },
    setAnwers () {
      this.preguntas.forEach((pregunta, index) => {
        this.returnToZero[index] = false
        this.returnToZero70 = false
        if (index === 35) {
          if (pregunta === 0) {
            this.porciones[35] = 0
            this.returnToZero70 = true
          }
          this.respuestas[35] = {
            dia: pregunta,
            porcion: this.porciones[35]
          }
        }
        if (index === 36) {
          this.respuestas[36] = {
            dia: pregunta,
            porcion: 1
          }
        }
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
      for (let i = 0; i < 37; i++) {
        this.preguntas[i] = '1'
        this.porciones[i] = 0
        this.returnToZero70 = false
      }
      this.preguntas[35] = 0
    }
  },
  components: {
    'template-one': templateOne,
    'template-two': templateTwo,
    'template-two-slider': templateTwoSlider
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
