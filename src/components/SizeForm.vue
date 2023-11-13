<template>
    <div>
        <div>
            <form id="size-form" @submit="createBuerger">
        <Message :msg="msg" v-show="msg" />
                <div class="input-container">
                    <label for="nome">Nome do Cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o pão do seu buerger:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Seleciona o tipo pão</option>
                        <option v-for="pao in paes" :key="pao._id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                 <div class="input-container">
                    <label for="carne">Escolha a carne do seu buerger:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Seleciona o tipo carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                    </select>
                </div>
                 <div class="input-container">
                    <label for="opcionais" id="opcionais-title">Seleciona os opcionais:</label>
                    <div class="checkbox-container" id="opcionais-container" v-for="opcionaisItem in opcionaisData" :key="opcionaisItem.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcionaisItem.tipo">
                        <span>{{opcionaisItem.tipo}}</span>
                    </div>
                </div>
                 <div class="input-container">
                    <label for="bebidas">Escolha a sua bebida:</label>
                    <select name="bebidas" id="bebidas" v-model="bebida">
                        <option value="">Seleciona o tipo bebida</option>
                        <option v-for="bebida in bebidas" :key="bebida.id" :value="bebida.tipo">{{bebida.tipo}}</option>
                    </select>
                </div>
                 <div class="input-container">
                    <label for="acompanhastes">Escolha o acompanhante do seu buerger:</label>
                    <select name="acompanhastes" id="acompanhastes" v-model="acompanhante">
                        <option value="">Seleciona o tipo de acompanhante</option>
                        <option v-for="acompanhante in acompanhantes" :key="acompanhante.id" :value="acompanhante.tipo">{{acompanhante.tipo}}</option>
                    </select>
                </div>
                 <div class="input-container">
                    <input type="submit" value="criar meu Buerger" class="submit-btn">
                </div>
            </form>
        </div>
    </div>

</template> 

<script>
import Message from './Message.vue'
import api from '../db/api'

export default {
    name: "SizeForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisData: null,
            bebidas: null,
            acompanhantes: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            bebida: null,
            acompanhante: null,
            status: "Solicitado",
            msg: null

        }
    },
    methods: {

        async getIngredientes() {

            await api
             .get("/paes")
                .then((res) => {
                    this.paes = res.data;
                })
                .catch((error) => {
                        console.log(error);
                });

            await api
             .get("/carnes")
                .then((res) => {
                    this.carnes = res.data;
                })
                .catch((error) => {
                        console.log(error);
                });

            await api
             .get("/opcionais")
                .then((res) => {
                    this.opcionaisData = res.data;
                })
                .catch((error) => {
                        console.log(error);
                });

            await api
             .get("/bebidas")
                .then((res) => {
                    this.bebidas = res.data;
                })
                .catch((error) => {
                        console.log(error);
                });

            await api
             .get("/acompanhante")
                .then((res) => {
                    this.acompanhantes = res.data
                })
                .catch((error) => {
                        console.log(error);
                });

                   
        },
        async createBuerger(e) {
            e.preventDefault()
           
            await api
                .post("/buergers", 
                {
                        nome: this.nome,
                        pao: this.pao,
                        carne: this.carne,
                        opcionais: Array.from(this.opcionais),
                        bebida: this.bebida,
                        acompanhante: this.acompanhante,
                        status: "Solicitado"
                }).then((res) => {
                    const id = res.data.response._id.substr(21, 22)
                    this.msg = `Pedido Nª ${id} realizado com sucesso!`;
                    setTimeout(() => this.msg = "", 3000)
                }).catch((error) => {
                    console.log(error)
                })
            
            this.nome = "",
            this.pao = "",
            this.carne = "",
            this.opcionais = "",
            this.bebida = "",
            this.acompanhante = ""

            window.scroll({
                top: 4,
                behavior: 'auto'
            })

        }
    },
    mounted() {
        this.getIngredientes()
    },
    components: {
        Message
    }
}
</script>

<style scoped>
    #size-form {
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #0c60b4;
        padding: 5px 10px;
        border-left: 4px solid #ffb89a;
    }
    input, select {
        padding: 5px 10px;
        width: 300px;
    }
    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }
    #opcionais-title {
        width: 100%;
    }
    .checkbox-container {
        display: flex;
        justify-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }
    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }
    .checkbox-container span {
        margin-left: 10px;
        font-weight: bold;
    }
    .submit-btn {
        background-color: #ffb89a;
        color: #0c60b4;
        font-weight: bold;
        border: 2px solid #f8cfbe;
        padding: 10px;
        font-size: 16px;
        transition: .5s;
        cursor: pointer;
    }
    .submit-btn:hover {
        background-color: transparent;
        color: #f8cfbe;
    }
</style>