<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-display-1 text-white">
            <span class="q-display-1">Calculadora de sodio 31/01/2022 - BBL </span>
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading">
          El sodio que consumimos diariamente proviene principalmente de la sal agregada a los alimentos procesados, empaquetados o
          aquellos preparados fuera de casa, como en restaurantes o establecimientos en la calle y, en menor cantidad, de la sal que usamos para cocinar.
          Si quiere saber cuánto sodio come habitualmente en un día, de manera aproximada, conteste la siguiente encuesta.
          <br/>
          <br/>
          <br/>
          <div class="q-headline text-secondary text-weight-bold q-mb-lg">Instrucciones de llenado</div>
          Lea atentamente las indicaciones escritas al inicio de cada sección, en ellas se proporciona información general del tipo de alimento que se está evaluando.
          En todas las preguntas, excepto las últimas dos, deberá proporcionar dos respuestas:
          <br/>
          <ul class="q-subheading">
            <li class="q-mb-md">La primera es la frecuencia con la que consume el alimento del cual se pregunta, es decir, cuántas veces al año, al mes, a la semana o
              al día lo consume. Cuando elija una opción diferente a <span class="text-weight-bold">Nunca</span>,
              se activará una barra de desplazamiento para que de su segunda respuesta.</li>
            <li class="q-mb-md">La segunda es la cantidad que consume del alimento, la cual podrá seleccionar desplazando con el ratón el
              círculo que encontrará del lado izquierdo.</li>
          </ul>
          Esta encuesta tiene un total de cuatro secciones. Para tener una mejor estimación de su consumo de sodio,
          asegúrese de haber respondido todas las preguntas de cada una de ellas. Si no está seguro de haberlas respondido todas,
          podrá navegar entre las secciones usando los botones <span class="text-weight-bold">REGRESAR</span> y <span class="text-weight-bold">CONTINUAR</span>
          ubicados al final de cada pantalla.
          </div>
          <div class="row reverse">
            <q-btn label="Empezar"
                  color="secondary"
                  size="lg"
                  class="q-mt-lg"
                  align="right"
                  @click="nextPage()"/>
          </div>
        </q-card-main>
      </q-card>
      <div class="row q-mt-xl" style="width: 1300px; margin: auto;">
        <div class="q-mt-md col-12">Este proyecto se llevó a cabo gracias al financiamiento CONACYT No. SALUD-2016-C02-272561 y la colaboración de las siguientes instituciones:</div>
        <div class="row items-end">
        <div class="col-sm-2 col-xs-12"><img src="../statics/LogoINCICH.png" alt="LogoINCICH" class="logos q-ma-md"/></div>
          <div class="col-sm-9 col-xs-12 q-ml-md q-pl-xs q-mb-md"><div class="text-weight-bold">Instituto Nacional de Cardiología 'Ignacio Chávez'</div>Departamento de Sociomedicina y Departamento de Instrumentación Electromecánica</div>
        </div>
        <div class="row items-end">
        <div class="col-sm-2 col-xs-12"><img src="../statics/LogoINCMNSZ.png" alt="LogoINCMNSZ" class="logos q-ml-md q-mt-xs q-mr-xs"/></div>
          <div class="col-sm-9 col-xs-12 q-mb-md"><div class="text-weight-bold">Instituto Nacional de Ciencias Médicas y Nutrición 'Salvador Zubirán'</div>Departamento de Nefrología y Metabolismo Mineral y Departamento de Ciencia y Tecnología de Alimentos</div>
        </div>
      </div>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data: function () {
    return {
    }
  },
  methods: {
    nextPage: function () {
      this.$emit('router', 1)
    }
  }
}
</script>
