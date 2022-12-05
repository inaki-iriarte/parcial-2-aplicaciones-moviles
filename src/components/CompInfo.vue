<template>
    <v-container>
        <v-expansion-panels focusable>
            <v-expansion-panel>
                <v-expansion-panel-header @click="mostrarInfo">
                    ¿Cómo se calcula?
                </v-expansion-panel-header>
                <v-expansion-panel-content v-html="info">
                </v-expansion-panel-content>
            </v-expansion-panel>
        </v-expansion-panels>
    </v-container>
</template>

<script>
export default {
    name: 'CompInfo',

    data: () => ({
        estado: false,
        info: null,
    }),
    methods: {
        mostrarInfo: function() {
            if (!this.info) {
                this.info = "<p>El valor de tus compras en moneda extranjera se calcula en base al tipo de cambio del día del dólar oficial, más impuestos que aplique.</p> <p>Sobre las compras en moneda extranjera con tarjeta de crédito o débito se aplican los siguientes impuestos:</p> <ul><li>El 30% de la compra por el Impuesto PAÍS según la RG 4659/2020.</li> <li>El 45% de la compra por el Impuesto a las Ganancias según la RG 4815/2020.</li></ul> <p>Si tu compra o suscripción en moneda extranjera es un servicio digital, se aplican los siguientes impuestos:</p> <ul><li>El 8% de la compra por el Impuesto PAÍS según la RG 4659/2020.</li> <li>El 21% de la compra por el IVA según la RG 4240/2018.</li> <li>El 45% de la compra por el Impuesto a las Ganancias según la RG 4815/2020.</li> <li>Es posible que apliquen impuestos de ingresos brutos según la provincia correspondiente.</li></ul>";
            } else {
                this.info = null;
            }
        }
    }
  }
</script>

<style>
.v-expansion-panel-header,
.v-expansion-panel-header--active {
    font-family: 'Montserrat', sans-serif;
    font-weight: 700;
    font-size: 1.5rem;
    color: #1E1E1E;
}

.v-expansion-panel {
    background-color: #EFEFEF !important;
}

.v-expansion-panels {
    border-radius: 12px;
    width: 90%;
    margin: auto;
    border: 1px solid #808080;
    overflow: hidden;
}

.v-expansion-panel-header {
    padding: 1.5rem;
}

.v-expansion-panel-content {
    padding: 1rem 1.5rem;
    font-family: 'Hind', sans-serif;
    font-size: 1rem;
    color: #1E1E1E;
    display: block;
}

.v-expansion-panel-content p {
    padding: 1rem 0rem;
    margin-bottom: 0;
}

.v-expansion-panel-content ul {
    margin: 1rem 0;
}

.v-expansion-panel::before {
    box-shadow: none;
}

@media screen and (max-width: 780px) {
    .v-expansion-panels {
        width: 100%;
    }
}
</style>