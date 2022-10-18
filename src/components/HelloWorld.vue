<template>
  <v-container class="center">
    <h1 class="my-5">View Leasing</h1>
    <v-card style="background-color: white;" light outlined elevation="0" class="pa-0 ma-0 mb-3 center">
      <v-container align="center">
        <v-btn class="mx-2" color="orange" dark>
          Guia
        </v-btn>
        <v-btn class="mx-2" color="error" >
          Datos del prestamo
        </v-btn>
        <v-btn class="mx-2" color="primary" >
          Datos de gastos iniciales
        </v-btn>
        <v-btn class="mx-2" color="green" dark >
          Datos de gastos periodicos
        </v-btn>
        <v-btn class="mx-2" color="purple" dark>
          Datos de costo de oportunidad
        </v-btn>
      </v-container>
    </v-card>
    <v-card style="background-color: white;" light outlined>
      <v-container>
          <v-row>
            <!-- columna seccion datos del usuario -->
            <v-col class="4">
              <v-text-field
              type="number"
              v-for="item in itemsCol1" :key="item.id"
              class="my-2"
              dense hide-details
              :v-model="item.value"
              :label="item.valueLb"
              :placeholder="item.valuePh"
              outlined
              ></v-text-field>              
            </v-col>

            <!-- columna seccion datos de gastos iniciales -->
            <v-col class="4">
              <v-text-field
              type="number"
              v-for="item in itemsCol2" :key="item.id"
              class="my-2"
              dense hide-details
              :v-model="item.value"
              :label="item.valueLb"
              :placeholder="item.valuePh"
              outlined
              ></v-text-field>
            </v-col>
            
            <!-- columna seccion datos de gastos peridicos &&&& datos de cosoto de oportunidad -->
            <v-col class="4">
              <v-text-field
              type="number"
              class="my-2"
              dense hide-details
              label="Comisión Periodica"
              placeholder="0000.00"
              outlined
              ></v-text-field>
              <v-text-field
              type="number"
              class="my-2"
              dense hide-details
              label="Porcentaje de seguro riesgo"
              placeholder="0000.00"
              outlined
              ></v-text-field>
              <v-text-field
              type="number"
              class="mt-14"
              dense hide-details
              label="Tasa de descuento KS"
              placeholder="0000.00"
              outlined
              ></v-text-field>
              <v-text-field
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
    </v-card>
    <v-card outlined class="mt-3">
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
      itemsCol1 : [
        {
          id:1,
          value: 0,
          valuePh: "0000.00",
          valueLb:"Precio de venta del activo",
        },
        {
          id:2,
          value: 0,
          valuePh: "sample",
          valueLb:"N de añios",
        },
        {
          id:3,
          value: 0,
          valuePh: "sample",
          valueLb:"Frecuencia de pago",
        },
        {
          id:4,
          value: 0,
          valuePh: "sample",
          valueLb:"N de dias por año",
        },
        {
          id:5,
          value: 0,
          valuePh: "sample",
          valueLb:"% de TEA",
        },
        {
          id:6,
          value: 0,
          valuePh: "sample",
          valueLb:"% IGV",
        },
        {
          id:7,
          value: 0,
          valuePh: "sample",
          valueLb:"% Impuesto a la renta",
        },
        {
          id:8,
          value: 0,
          valuePh: "sample",
          valueLb:"% de recompra",
        },
      ],
      itemsCol2: [
        {
          id: 1,
          value: 0   ,
          valueLb: "Costes Notariales" ,
          valuePh: "0000.00" ,
        },
        {
          id: 2,
          value: 0   ,
          valueLb: "Costes Registrales" ,
          valuePh: "0000.00" ,
        },
        {
          id: 3,
          value: 0   ,
          valueLb: "Tasación" ,
          valuePh: "0000.00" ,
        },
        {
          id: 4,
          value: 0   ,
          valueLb: "Comisión de Estudio" ,
          valuePh: "0000.00" ,
        },
        {
          id: 5,
          value: 0   ,
          valueLb: "Comisión de Activación" ,
          valuePh: "0000.00" ,
        },
      ],
      headers: [
          { text: 'N°', align: 'start', sortable: false, value: 'name' },
          { text: 'P.G.', value: 'calories' },
          { text: 'Saldo Inicial', value: 'fat' },
          { text: 'Interes', value: 'carbs' },
          { text: 'Cuota', value: 'protein' },
          { text: 'Amort.', value: 'iron' },
          { text: 'Seguro Interno', value: 'iron' },
          { text: 'Comision', value: 'iron' },
          { text: 'Recompesa', value: 'iron' },
          { text: 'Saldo Final', value: 'iron' },
        ],
        desserts: [
          {
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0,
            iron: '1%',
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3,
            iron: '1%',
          },
          {
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0,
            iron: '7%',
          },
          {
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3,
            iron: '8%',
          },
          {
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9,
            iron: '16%',
          },
          {
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0,
            iron: '0%',
          },
          {
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0,
            iron: '2%',
          },
          {
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5,
            iron: '45%',
          },
          {
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9,
            iron: '22%',
          },
          {
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7,
            iron: '6%',
          },
        ],
    }),
  }
</script>
