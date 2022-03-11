<template>
  <q-page padding>
    <div class="row">
      <q-card style="width: 1300px; margin: auto; background-color: white">
        <q-card-title class="bg-secondary">
          <div class="q-title q-headline text-white">
            <span class="q-display-1">Su consumo habitual de sodio</span>
          </div>
        </q-card-title>
        <q-card-separator />
        <q-card-main>
          <div class="q-subheading q-mt-lg">
            La Organización Mundial de la Salud recomienda un consumo máximo de 2000 mg/día de sodio para adultos. Usted consume aproximadamente <span class="text-weight-bold ">{{ Math.round(resultadoFinal * 100) / 100 }} mg</span> de sodio al día.
          </div>
          <div v-if="diferenciaSodio > 0" class="q-subheading q-mt-md">
            Su consumo está un {{ Math.round(PDiferenciaSodio * 100) / 100 }} % por arriba del límite máximo recomendado.
          </div>
          <div v-else class="q-subheading q-mt-md">
            ¡Muy bien! su consumo de sodio se encuentra dentro del nivel recomendado.
          </div>

          <div class="q-subheading q-mt-md">
            <span class="text-weight-bold ">{{ Math.round(PSodio1_2 * 100) / 100 }} %</span> de su consumo diario de sodio proviene de alimentos preparados fuera de casa.
          </div>
          <div class="q-subheading q-mt-md">
            <span class="text-weight-bold ">{{ Math.round(PSodio3 * 100) / 100 }} %</span> de su consumo diario de sodio proviene de helados, postres, repostería, panadería y galletas.
          </div>
          <div class="q-subheading q-mt-md">
            <span class="text-weight-bold ">{{ Math.round(PSodio4 * 100) / 100 }} %</span> de su consumo diario de sodio proviene de alimentos procesados.
          </div>
          <div class="q-subheading q-mt-md">
            <span class="text-weight-bold ">{{ Math.round(PSodio5 * 100) / 100 }} %</span> de su consumo diario de sodio proviene de la sal de mesa, condimentos y sazonadores salados, así como de salsas picantes (botaneras) que agrega a sus alimentos.
          </div>

          <div class="row reverse">
            <q-btn-group class="q-mt-xl">
              <q-btn label="Reiniciar"
                color="secondary"
                size="lg"
                @click="reiniciar()"/>
              <q-btn label="Salir"
                color="red"
                size="lg"
                @click="salir()"/>
            </q-btn-group>
          </div>
        </q-card-main>
      </q-card>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Results',
  props: [
    'parteUno',
    'parteDos',
    'parteTres',
    'parteCuatro',
    'valores',
    'calcular'
  ],
  data () {
    return {
      resultados: [],
      resultados1_2: [],
      resultados3: [],
      resultados4: [],
      resultado1_2: 0,
      resultado3: 0,
      resultado4: 0,
      resultado5: 0,
      resultadoFinal: 0,
      diferenciaSodio: 0,
      PDiferenciaSodio: 0,
      PSodio1_2: 0,
      PSodio3: 0,
      PSodio4: 0,
      PSodio5: 0
    }
  },
  methods: {
    getResult () {
      this.resultados = this.parteUno.concat(this.parteDos, this.parteTres, this.parteCuatro)
      this.valores.forEach((value, index) => {
        console.log('--------------------------------')
        console.log('Pregunta ' + (index + 1))
        console.log('resultado antes ' + this.resultadoFinal)
        this.resultadoFinal += this.resultados[index].dia * this.resultados[index].porcion * value
        console.log('valor ' + value)
        console.log('dia ' + this.resultados[index].dia)
        console.log('porcion ' + this.resultados[index].porcion)
        console.log('operacion ' + this.resultados[index].dia * this.resultados[index].porcion * value)
        console.log('resultado despues ' + this.resultadoFinal)
        if (index < 25) {
          this.resultado1_2 += this.resultados[index].dia * this.resultados[index].porcion * value
        } else if (index < 34) {
          this.resultado3 += this.resultados[index].dia * this.resultados[index].porcion * value
        } else if (index === 56 || index === 57 || index === 58 || index === 69 || index === 70) {
          this.resultado5 += this.resultados[index].dia * this.resultados[index].porcion * value
        } else {
          this.resultado4 += this.resultados[index].dia * this.resultados[index].porcion * value
        }
      })
      this.diferenciaSodio = this.resultadoFinal - 2000
      if (this.diferenciaSodio > 0) {
        this.PDiferenciaSodio = this.diferenciaSodio / 2000 * 100
      }
      if (this.resultadoFinal !== 0) {
        this.PSodio1_2 = this.resultado1_2 / this.resultadoFinal * 100
        this.PSodio3 = this.resultado3 / this.resultadoFinal * 100
        this.PSodio4 = this.resultado4 / this.resultadoFinal * 100
        this.PSodio5 = this.resultado5 / this.resultadoFinal * 100
      }
    },
    salir () {
      this.$emit('exit', true)
      // window.top.close()
    },
    reiniciar () {
      location.reload()
    }
  },
  components: {
  },
  watch: {
    calcular: function () {
      this.getResult()
    }
  }
}
</script>

<style>
</style>
