<template>
  <v-container
    id="regular-tables"
    fluid
    tag="section"
  >
    <v-row no-gutters>
      <v-col
        cols="12"
        sm="6"
        md="4"
      >
        <v-card
          class="pa-2"
          tile
        >
          <v-img
            :src="'data:image/jpeg;base64,'+foto"
            max-height="370"
            contain
            class="grey darken-4"
          />
        </v-card>
      </v-col>
      <v-col
        cols="6"
        md="4"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
          <v-text-field
            v-model="dni"
            label="N° Identity Document"
            type="number"
          />
          <v-btn
            color="secondary"
            class="mr-0"
            @click="testing"
          >
            Search Visitor
          </v-btn>
          <v-text-field
            v-model="nombre"
            label="Name"
            disabled
          />

          <v-text-field
            v-model="apellidoPaterno"
            label="Last Name"
            disabled
          />
          <v-text-field
            v-model="apellidoMaterno"
            label="Mother's last name"
            disabled
          />
          <v-text-field
            v-model="fechaNac"
            label="Date of birth"
            disabled
          />
        </v-card>
      </v-col>
    </v-row>
    <base-v-component
      heading="Simple Tables"
      link="components/simple-tables"
    />

    <base-material-card
      icon="mdi-account-search-outline"
      title="Visitors List"
      class="px-5 py-3"
    >
      <v-simple-table>
        <thead>
          <tr>
            <th class="primary--text">
              ID
            </th>
            <th class="primary--text">
              Name
            </th>
            <th class="primary--text">
              Country
            </th>
            <th class="primary--text">
              City
            </th>
            <th class="text-right primary--text">
              Salary
            </th>
          </tr>
        </thead>

        <tbody>
          <tr>
            <td>1</td>
            <td>Dakota Rice</td>
            <td>Niger</td>
            <td>Oud-Turnhout</td>
            <td class="text-right">
              $36,738
            </td>
          </tr>

          <tr>
            <td>2</td>
            <td>Minverva Hooper</td>
            <td>Curaçao</td>
            <td>Sinaas-Waas</td>
            <td class="text-right">
              $23,789
            </td>
          </tr>

          <tr>
            <td>3</td>
            <td>Sage Rodriguez</td>
            <td>Netherlands</td>
            <td>Baileux</td>
            <td class="text-right">
              $56,142
            </td>
          </tr>

          <tr>
            <td>4</td>
            <td>Philip Chaney</td>
            <td>Korea, South</td>
            <td>Overland Park</td>
            <td class="text-right">
              $38,735
            </td>
          </tr>

          <tr>
            <td>5</td>
            <td>Doris Greene</td>
            <td>Malawi</td>
            <td>Feldkirchen in Kärnten</td>
            <td class="text-right">
              $63,542
            </td>
          </tr>

          <tr>
            <td>6</td>
            <td>Mason Porter</td>
            <td>Chile</td>
            <td>Gloucester</td>
            <td class="text-right">
              $78,615
            </td>
          </tr>
        </tbody>
      </v-simple-table>
    </base-material-card>
  </v-container>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        tipoDocumentoOptions: ['DNI', 'CE'],
        sexoOptions: [],
        lenguaOptions: [],
        lenguaMaterna: '',
        tipo: '',
        tipoDocumento: '',
        sexo: '',
        dni: '',
        nombre: '',
        apellidoPaterno: '',
        apellidoMaterno: '',
        fechaNac: '',
        descripcion: '',
        direccion: '',
        isBusy: false,
        foto: '',
      }
    },
    methods: {
      async testing () {
        const data = await axios.get('http://www.csjarequipa.gob.pe/sioj/WebServiceKn.php?Id=' + this.dni)
        // eslint-disable-next-line no-eval
        const dataObjetc = eval(data.data)
        const dataJson = (dataObjetc[0])
        this.nombre = dataJson.NOMBRE
        this.apellidoPaterno = dataJson.APP
        this.apellidoMaterno = dataJson.APM
        this.sexo = dataJson.sexo
        this.estadoCivil = dataJson.estadoc
        this.fechaNac = dataJson.fechanac
        this.edad = dataJson.edad
        this.direccion = dataJson.nomb_dire
        this.foto = dataJson.FOTO
      },
    },
  }
</script>
