<template>
    <div id="calculos">
        <v-card>
            <v-container>
                <v-row>
                    <v-col>
                        <h4>Porcentagem do Orçamentopara cada Área</h4>
                        <v-text-field class="orcArea" disabled label="Tecnológica %" id="porcentagemPorArea" v-model.number="porcentagemTecnologica"></v-text-field>
                        <v-text-field class="orcArea" disabled label="Médica %" id="porcentagemPorArea" v-model.number="porcentagemMedica"></v-text-field>
                        <v-text-field class="orcArea" disabled label="Humanas %" id="porcentagemPorArea" v-model.number="porcentagemHumana"></v-text-field>
                    </v-col>
                    <v-col>
                        <h4>Top 5 Projetos mais caros</h4>
                        <table class="tableTop5">
                            <tr>
                                <th>Posição</th>
                                <th>Nome</th> 
                                <th>Orçamento</th>      
                            </tr>
                            <tr class='tableTop5' v-for="(p, idx) in top5" :key="idx">
                                <td id='idx'>{{idx + 1 + 'º'}}</td>
                                <td id='nome'>{{p.nome}}</td>
                                <td id='orcamento'>{{p.orcamento}}</td>
                            </tr>
                        </table>
                    </v-col>
                    <v-col>
                        <h4>Orçamento Total</h4>
                        <v-text-field label="Total geral R$" disabled id="porcentagemTotal" v-model.number="totalOrcamentoGeral"></v-text-field>
                    </v-col>
                </v-row>
            </v-container> 
        </v-card>        
    </div>
</template>


<script>
import axios from 'axios'

export default {
    props: {
        areas: Array,
    },

    data() {
        return {
            porcentagemTecnologica: 0,
            porcentagemMedica: 0,
            porcentagemHumana: 0,
            totalOrcamentoGeral: 0,
            totalOrcamentoTec: 0,
            totalOrcamentoHum: 0,
            totalOrcamentoMed: 0,
            top5: [],
        }
    },
    mounted() {
        axios.get('https://projeto-prova.herokuapp.com/projeto').then(response => {
            this.areas = response.data
            this.somarOrcamentos()
            this.calcularPorcentagemAreas()
            this.setarTop5()
        })
    },
    methods: {
        somarOrcamentos() {
            for (var i = 0; i < this.areas.length; i++) {
                this.totalOrcamentoGeral += this.areas[i].orcamento
                
                if (this.areas[i].area == 'TECNOLOGICA') {
                    this.totalOrcamentoTec += this.areas[i].orcamento
                }

                if (this.areas[i].area == 'HUMANA') {
                    this.totalOrcamentoHum += this.areas[i].orcamento
                }

                if (this.areas[i].area == 'MEDICA') {
                    this.totalOrcamentoMed += this.areas[i].orcamento
                }
            }
        },
        calcularPorcentagemAreas() {
            this.porcentagemTecnologica = parseFloat((this.totalOrcamentoTec * 100) / this.totalOrcamentoGeral).toFixed(2)
            this.porcentagemMedica = parseFloat((this.totalOrcamentoMed * 100) / this.totalOrcamentoGeral).toFixed(2)
            this.porcentagemHumana = parseFloat((this.totalOrcamentoHum * 100) / this.totalOrcamentoGeral).toFixed(2)
        },
        setarTop5() {
            const areasOrdenadas = this.areas.sort(function(a, b) {
                if(a.orcamento > b.orcamento) return -1;
                if(a.orcamento < b.orcamento) return 1;
                return 0;  
            });
            
            this.top5 = areasOrdenadas.slice(0, 5);
        },
    }

}
</script>

<style>

.v-text-field {
    width: 100%;
}

label{
    width: 43%;
    text-align: right;
}

.v-col {
    align-items: center;
}

.orcArea {
    box-shadow: 0 0 0 0;
    border: 0 none;
    outline: 0;
}

table, th, td {
  border: 1px solid slategray;
  border-collapse: collapse;
  position: f;
}

td {
    margin-left: 1px;
}

table {
  width: 40%;
  margin-left: 30%;
  margin-top: 1%;
}

</style>