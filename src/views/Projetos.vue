<template>
    <div id="projetos">
        <h1>Adicione seu Projeto</h1>
        <form v-on:submit.prevent = "addProjeto()">
            <v-card>
                <v-container>
                    <v-row>
                        <v-col>
                            Área*
                            <select required v-model="novoProjeto.area">
                                <option v-for="(a, idx) in areas" :key="idx">{{a.nome}}</option>
                            </select>
                        </v-col>
                        <v-col>
                            <v-text-field id="nome" placeholder="Nome*" required v-model="novoProjeto.nome"></v-text-field>
                        </v-col>
                        <v-col>
                            <v-text-field id="prazo" placeholder="Prazo em dias*" required v-model="novoProjeto.prazo"></v-text-field>
                        </v-col>
                        <v-col>
                            <v-text-field id="orcamento" placeholder="Orçamento em reais*" required @change="verificarOrcamento()" v-model="novoProjeto.orcamento"></v-text-field>
                        </v-col>
                    </v-row>
                    <small>*Indica campos obrigatórios</small>
                </v-container> 
            </v-card>
            <div class="divBtn">
                <button class="button" type="submit">Adicionar</button> 
            </div>
        </form>
    </div>
</template>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            areas: [
                {nome: 'TECNOLOGICA'},
                {nome: 'HUMANAS'},
                {nome: 'MEDICA'},
            ],
            novoProjeto: {
                id: '',
                nome: '',
                area: '',
                prazo: '',
                orcamento: '',
            }
        }
    },
    methods: {
        addProjeto() {
            axios.post('https://projeto-prova.herokuapp.com/projeto', this.novoProjeto).then(response => {
                this.novoProjeto.id = response.data
                alert('Novo projeto criado com sucesso!')
            }).catch(error => alert('Error:' + error))

            this.novoProjeto.nome = ''
            this.novoProjeto.area = ''
            this.novoProjeto.prazo = ''
            this.novoProjeto.orcamento = ''

        },
        verificarOrcamento() {
            let action = ''
            if ((this.novoProjeto.orcamento > 0 && this.novoProjeto.orcamento < 5000) || this.novoProjeto.orcamento > 100000) {
                action = confirm('O orçamento deve estar entre 5.000,00 e 100.000,00')
            }

            if (action == true) {
                this.novoProjeto.orcamento = ''
            }
        }
    }
}
</script>

<style>
#projetos {
    padding: 2em;
}

.col {
    padding: 2px;
    width: 100%;
}

.divBtn {
    margin-top: 2em;
}

</style>