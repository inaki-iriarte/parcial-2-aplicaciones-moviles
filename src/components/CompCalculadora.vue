<template>
    <v-container>
        <h1>¿Cuánto es?</h1>
        <p class="subtitulo">Calculadora de impuestos en compras con moneda extranjera</p>

        <div id="calc">
            <div class="container-calc">
                <label for="compra" class="inst">Ingrese su compra con su costo (puede ser más de una)</label>
        
                <div class="ingreso-compra">
                    <span>
                        <img v-if="selected == 'ars'" :src="imagenARS" alt="AR">
                        <img v-if="selected == 'usd'" :src="imagenUSD" alt="US">
                    </span>
                    <select name="moneda" id="moneda-select" v-model="selected" @change="nuevaMoneda">
                        <option value="ars">ARS</option>
                        <option value="usd">USD</option>
                    </select>
                    <input type="number" placeholder="Ingrese el costo de la compra" step="0.01" id="compra"
                        @keyup.enter="agregarCompra" v-model="compra">
                    <button @click="agregarCompra">Agregar</button>
                </div>

                <label for="compra-tipo" class="label-tipo">Seleccione el tipo de compra:</label>
                <select name="compra-tipo" id="compra-tipo" v-model="tipoCompra" class="compra-tipo">
                    <option value="Compra">Compra</option>
                    <option value="Servicio">Servicio</option>
                    <option value="Compra/Servicio Digital">Compra/servicio digital</option>
                    <option value="Suscripcion">Suscripcion digital</option>
                    <option value="Turismo">Pasaje o paquete turístico</option>
                    <option value="Otro">Otros</option>
                </select>

                <div class="listado">
                    <template v-if="listaCompras.length">
                        <ul>
                            <li v-for="(compra, index) in listaCompras" :key="compra.id">
                                <span class="listado-tipo">{{compra.tipo}}</span>
                                <span class="compras">
                                    <span v-if="selected == 'ars'">ARS</span>
                                    <span v-if="selected == 'usd'">USD</span>
                                    {{compra.valor}}
                                    <img :src="require('../assets/bin.svg')" alt="Eliminar" class="borrar" @click="eliminarCompra">
                                </span>
                                <span class="index">{{index}}</span>
                            </li>
                        </ul>
                
                        <hr>
                
                        <p>Subtotal <span>ARS {{subtotal}}</span></p>
                        <p>+ Impuesto PAÍS <span>ARS {{impPais}}</span></p>
                        <p>+ Imp. a las Ganancias <span>ARS {{impGanancias}}</span></p>
                
                        <hr>
                
                        <p id="total">Total con impuestos <span>ARS {{total}}</span></p>
                    </template>
                </div>
            </div>
        </div>
    </v-container>
</template>

<script>
export default {
    name: 'CompCalculadora',

    data: () => ({
        selected: 'ars',
        index: false,
        imagenARS: require('../assets/AR.png'),
        imagenUSD: require('../assets/US.png'),
        tipoCompra: 'Compra',
        compra: '',
        listaCompras: [],
        dolar: 0,
        subtotalUSD: 0,
        subtotal: 0,
        impPais: 0,
        impGanancias: 0,
        total: 0
    }),
    methods: {
        agregarCompra: function() {
            let objetoCompra = {};
            objetoCompra.valor = this.compra;
            objetoCompra.tipo = this.tipoCompra;
            this.subtotal += parseFloat(this.compra);
            if (this.selected == 'usd') {
                this.subtotalUSD += parseFloat(this.compra);
                this.subtotal = parseFloat((this.subtotalUSD*this.dolar).toFixed(2));
            }
            this.impPais = parseFloat((this.subtotal*0.3).toFixed(2));
            this.impGanancias = parseFloat((this.subtotal*0.45).toFixed(2));
            this.total = parseFloat((this.subtotal + this.impGanancias + this.impPais).toFixed(2));

            this.listaCompras.push(objetoCompra);
            this.compra = "";
            this.tipoCompra = 'Compra';
        },
        nuevaMoneda: function() {
            this.listaCompras = [];
            this.subtotal = 0;
            this.subtotalUSD = 0;
            this.impPais = 0;
            this.impGanancias = 0;
            this.total = 0;
        },
        eliminarCompra: function(e) {
            let i = e.target.parentElement.nextElementSibling.innerHTML;
            if (this.selected == 'usd') {
                this.subtotalUSD = parseFloat((this.subtotalUSD - this.listaCompras[i].valor).toFixed(2));
                this.subtotal = parseFloat((this.subtotalUSD*this.dolar).toFixed(2));
            } else {
                this.subtotal = parseFloat((this.subtotal - this.listaCompras[i].valor).toFixed(2));
            }
            this.impPais = parseFloat((this.subtotal*0.3).toFixed(2));
            this.impGanancias = parseFloat((this.subtotal*0.45).toFixed(2));
            this.total = parseFloat((this.subtotal + this.impPais + this.impGanancias).toFixed(2));

            this.listaCompras.splice(i, 1);
        },
    }
  }
</script>

<style>
* {
    box-sizing: border-box;
}

.container {
    font-family: 'Montserrat', sans-serif;
}

h1{
  margin: 0;
  font-weight: 700;
  font-size: 3rem;
  text-align: center;
  color: #1E1E1E;
}

.subtitulo{
  color: #154C6B;
  font-weight: 400;
  font-size: 1.5rem;
  text-align: center;
}

#calc{
  width: 90%;
  margin: auto;
}

.container-calc{
  border: 1px solid #808080;
  border-radius: 12px;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
}

.inst{
  font-weight: 600;
  font-size: 1.5rem;
  color: #154C6B;
  margin-bottom: 1rem;
}

.ingreso-compra{
  border: 2px solid #1A6484;
  border-radius: 10px;
  height: 50px;
  display: flex;
  overflow: hidden;
}

.ingreso-compra input{
  width: 70%;
  border: none;
  border-left: 2px solid #1A6484;
  padding: 0 1rem;
  outline: none;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  font-size: 1rem;
  background-color: #EFEFEF;
  appearance: textfield;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.ingreso-compra select{
  border: none;
  background-color: #CAE4EF;
  font-weight: 700;
  font-size: 1.2rem;
  font-family: 'Montserrat', sans-serif;
  padding: 0 0.5rem;
  appearance: menulist !important;
}

.ingreso-compra span{
  background-color: #CAE4EF;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 10px;
}

.ingreso-compra span img{
  width: 32px;
  height: 32px;
}

.ingreso-compra button{
  border: none;
  background-color: #EFEFEF;
  border-left: 2px solid #1A6484;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  cursor: pointer;
  padding: 0 1rem;
  width: 25%;
}

.label-tipo{
  margin: 0.5rem 0;
  color: #154C6B;
  font-weight: 600;
}

.compra-tipo{
  background-color: #EFEFEF;
  border: 2px solid #1A6484;
  border-radius: 5px;
  padding: 0.5rem;
  font-family: 'Montserrat', sans-serif;
  font-size: 1rem;
  font-weight: 600;
  appearance: menulist !important;
}

hr{
  width: 95%;
  background-color: #808080;
  margin: 0.5rem 0;
}

.listado{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.listado ul{
  width: 100%;
  margin: 1rem 0;
}

.listado ul li{
  font-size: 1.2rem;
  width: 100%;
  margin: 0.2rem 0;
  font-family: 'Hind', sans-serif;
  display: flex;
  justify-content: space-between;
}

.compras{
  margin-right: 40px;
  font-weight: 600;
}

.borrar{
  width: 18px;
  height: 18px;
}
.borrar:hover{
  cursor: pointer;
}

.index{
  display: none;
}

.listado p {
  width: 90%;
  font-family: 'Hind', sans-serif;
  font-weight: 600;
  font-size: 1.2rem;
  margin: 0.5rem 0;
  display: flex;
  justify-content: space-between;
}

.listado p span{
  font-weight: 700;
}

#total{
  width: 95%;
  background-color: #266ABC;
  padding: 1rem;
  border-radius: 12px;
  color: white;
  font-size: 1.5rem;
}
</style>