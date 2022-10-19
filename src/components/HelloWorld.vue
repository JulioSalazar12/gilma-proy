<template>
  <v-container class="center">
    <h1 class="my-5">View Leasing</h1>
    <v-card style="background-color: white;" light outlined elevation="0" class="pa-0 ma-0 mb-3 center">
      <v-container align="center">
        <v-btn elevation="0" class="mx-2" color="orange" dark>
          Guia
        </v-btn>
        <v-btn elevation="0" class="mx-2" color="error" >
          Datos del prestamo
        </v-btn>
        <v-btn elevation="0" class="mx-2" color="primary" >
          Datos de gastos iniciales
        </v-btn>
        <v-btn elevation="0" class="mx-2" color="green" dark >
          Datos de gastos periodicos
        </v-btn>
        <v-btn elevation="0" class="mx-2" color="purple" dark>
          Datos de costo de oportunidad
        </v-btn>
      </v-container>
    </v-card>
    <v-card style="background-color: white;" light outlined>
      <v-form 
        ref="form"
        v-model="valid"
        lazy-validation>
        <v-container>
            <v-row>
              <!-- columna seccion datos del usuario -->
              <v-col class="4">
                <v-text-field                
                required
                :rules="nameRules"
                type="number"
                v-for="item in itemsCol1" :key="item.id"
                class="my-2"
                dense hide-details
                v-model="item.value"
                :label="item.valueLb"
                :placeholder="item.valuePh"
                outlined
                ></v-text-field>              
              </v-col>

              <!-- columna seccion datos de gastos iniciales -->
              <v-col class="4">
                <v-text-field
                required
                :rules="nameRules"
                type="number"
                v-for="item in itemsCol2" :key="item.id"
                class="my-2"
                dense hide-details
                v-model="item.value"
                :label="item.valueLb"
                :placeholder="item.valuePh"
                outlined
                ></v-text-field>
              </v-col>
              
              <!-- columna seccion datos de gastos peridicos &&&& datos de cosoto de oportunidad -->
              <v-col class="4">
                <v-text-field
                v-model="dataCP"
                required
                :rules="nameRules"
                type="number"
                class="my-2"
                dense hide-details
                label="Comisión Periodica"
                placeholder="0000.00"
                outlined
                ></v-text-field>
                <v-text-field
                v-model="dataPSR"
                required
                :rules="nameRules"
                type="number"
                class="my-2"
                dense hide-details
                label="Porcentaje de seguro riesgo"
                placeholder="0000.00"
                outlined
                ></v-text-field>
                <v-text-field
                v-model="dataTdKS"
                required
                :rules="nameRules"
                type="number"
                class="mt-14"
                dense hide-details
                label="Tasa de descuento KS"
                placeholder="0000.00"
                outlined
                ></v-text-field>
                <v-text-field
                v-model="dataWACC"
                required
                :rules="nameRules"
                type="number"
                class="my-2"
                dense hide-details
                label="Tasa de descuento WACC"
                placeholder="0000.00"
                outlined
                ></v-text-field>                           
                <v-container>
                  <v-row style="height:145px;">
                    <v-col align-self="end">
                      <v-btn
                        dark
                      color="orange"
                      @click="validate"
                      block elevation="0">
                      <v-icon class="mr-3">mdi-table-sync</v-icon>
                        Generar Tabla
                        </v-btn>
                    </v-col>
                    <v-col align-self="end">
                      <v-btn
                        dark
                      color="orange"
                      block elevation="0">
                        <v-icon class="mr-3">mdi-play</v-icon>
                        Ver resultados
                      </v-btn>
                    </v-col>
                  </v-row>
                </v-container>
              </v-col>
            </v-row>
        </v-container>
      </v-form>
    </v-card>
    <v-card v-if="enableValue" outlined class="mt-3">
      <v-data-table
        :headers="headers"
        :items="desserts"
        :items-per-page="5"
      ></v-data-table>
    </v-card>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      valid: true,
      enableValue: false,
      nameRules: [v => !!v],
      itemsCol1 : [
        {
          id:1,
          value: "",
          valuePh: "0000.00",
          valueLb:"Precio de venta del activo",
        },
        {
          id:2,
          value: "",
          valuePh: "sample",
          valueLb:"N de años",
        },
        {
          id:3,
          value: "",
          valuePh: "sample",
          valueLb:"Frecuencia de pago",
        },
        {
          id:4,
          value: "",
          valuePh: "sample",
          valueLb:"N de dias por año",
        },
        {
          id:5,
          value: "",
          valuePh: "sample",
          valueLb:"% de TEA",
        },
        {
          id:6,
          value: "",
          valuePh: "sample",
          valueLb:"% IGV",
        },
        {
          id:7,
          value: "",
          valuePh: "sample",
          valueLb:"% Impuesto a la renta",
        },
        {
          id:8,
          value: "",
          valuePh: "sample",
          valueLb:"% de recompra",
        },
      ],
      itemsCol2: [
        {
          id: 1,
          value: ""   ,
          valueLb: "Costes Notariales" ,
          valuePh: "0000.00" ,
        },
        {
          id: 2,
          value: ""   ,
          valueLb: "Costes Registrales" ,
          valuePh: "0000.00" ,
        },
        {
          id: 3,
          value: ""   ,
          valueLb: "Tasación" ,
          valuePh: "0000.00" ,
        },
        {
          id: 4,
          value: ""   ,
          valueLb: "Comisión de Estudio" ,
          valuePh: "0000.00" ,
        },
        {
          id: 5,
          value: ""   ,
          valueLb: "Comisión de Activación" ,
          valuePh: "0000.00" ,
        },
      ],
      dataCP: "",
      dataPSR: "",
      dataTdKS: "",
      dataWACC: "",
      headers: [
          { text: 'N°',                 value: 'name', align: 'start', sortable: false },
          { text: 'P.G.',               value: 'dataPG' },
          { text: 'Saldo Inicial',      value: 'dataSI' },
          { text: 'Interes',            value: 'dataI' },
          { text: 'Cuota',              value: 'dataC' },
          { text: 'Amort.',             value: 'dataA' },
          { text: 'Seguro Riesgo',      value: 'dataSR' },
          { text: 'Comision',           value: 'dataComi' },
          { text: 'Recompra',           value: 'dataRecom' },
          { text: 'Saldo Final',        value: 'dataSF' },
          { text: 'Depreciación',       value: 'dataDepre' },
          { text: 'Ahorro Tributario',  value: 'dataAhoro' },
          { text: 'IGV',                value: 'dataIGV' },
          { text: 'Flujo Bruto',        value: 'dataFb' },
          { text: 'Flujo con IGV',      value: 'dataFIGV' },
          { text: 'Flujo Neto',         value: 'dataN' },
        ],
        desserts: [
          {
            name: '1',
            dataPG: 159,
            dataSI: 6.0,
            dataI: 24,
            dataC: 4.0,
            dataA: '1%',
            dataSR: '45.25',
            dataComi: '45.25',
            dataRecom: '45.25',
            dataSF: '45.25',
            dataDepre: '45.25',
            dataAhoro: '45.25',
            dataIGV: '45.25',
            dataFb: '45.25',
            dataFIGV: '45.25',
            dataN: '45.25',
          },
          {
            name: '1',
            dataPG: 159,
            dataSI: 6.0,
            dataI: 24,
            dataC: 4.0,
            dataA: '1%',
            dataSR: '45.25',
            dataComi: '45.25',
            dataRecom: '45.25',
            dataSF: '45.25',
            dataDepre: '45.25',
            dataAhoro: '45.25',
            dataIGV: '45.25',
            dataFb: '45.25',
            dataFIGV: '45.25',
            dataN: '45.25',
          },
          {
            name: '1',
            dataPG: 159,
            dataSI: 6.0,
            dataI: 24,
            dataC: 4.0,
            dataA: '1%',
            dataSR: '45.25',
            dataComi: '45.25',
            dataRecom: '45.25',
            dataSF: '45.25',
            dataDepre: '45.25',
            dataAhoro: '45.25',
            dataIGV: '45.25',
            dataFb: '45.25',
            dataFIGV: '45.25',
            dataN: '45.25',
          },
          {
            name: '1',
            dataPG: 159,
            dataSI: 6.0,
            dataI: 24,
            dataC: 4.0,
            dataA: '1%',
            dataSR: '45.25',
            dataComi: '45.25',
            dataRecom: '45.25',
            dataSF: '45.25',
            dataDepre: '45.25',
            dataAhoro: '45.25',
            dataIGV: '45.25',
            dataFb: '45.25',
            dataFIGV: '45.25',
            dataN: '45.25',
          },
          {
            name: '1',
            dataPG: 159,
            dataSI: 6.0,
            dataI: 24,
            dataC: 4.0,
            dataA: '1%',
            dataSR: '45.25',
            dataComi: '45.25',
            dataRecom: '45.25',
            dataSF: '45.25',
            dataDepre: '45.25',
            dataAhoro: '45.25',
            dataIGV: '45.25',
            dataFb: '45.25',
            dataFIGV: '45.25',
            dataN: '45.25',
          },
        ],
    }),
    methods: {
      validate () {
        let sample = {
          dataPVA:  parseInt(this.itemsCol1[0].value),
          dataNA:   parseInt(this.itemsCol1[1].value),
          dataFP:   parseInt(this.itemsCol1[2].value),
          dataNDA:  parseInt(this.itemsCol1[3].value),
          dataPTEA: parseInt(this.itemsCol1[4].value),
          dataIGV:  parseInt(this.itemsCol1[5].value),
          dataPIR:  parseInt(this.itemsCol1[6].value),
          dataPR:   parseInt(this.itemsCol1[7].value),
          dataCN:   parseInt(this.itemsCol2[0].value),
          dataCR:   parseInt(this.itemsCol2[1].value),
          dataT:    parseInt(this.itemsCol2[2].value),
          dataCE:   parseInt(this.itemsCol2[3].value),
          dataCA:   parseInt(this.itemsCol2[4].value),
          dataCP:   parseInt(this.dataCP),
          dataPSR:  parseInt(this.dataPSR),
          dataTdKS: parseInt(this.dataTdKS),  
          dataWACC: parseInt(this.dataWACC),  
        }
        if (this.$refs.form.validate()==true){
          console.log("Data POST:", sample);
          this.enableValue = true;
        }
        
      },      
    }
  }
</script>
