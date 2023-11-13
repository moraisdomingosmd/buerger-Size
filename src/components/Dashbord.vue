<template>
    <div id="burger-table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Bebida:</div>
                <div>Acompanhante:</div>
                <div>Ações:</div>
            </div>
            <div id="burger-table-rows">
                <div class="burger-table-row" v-for="dado in dados" :key="dado._id">
                    <div class="order-number">{{dado._id.substr(21, 22)}}</div>
                    <div>{{dado.nome}}</div>
                    <div>{{dado.pao}}</div>
                    <div>{{dado.carne}}</div>
                    <div>
                        <ul>
                            <li v-for="(opcional, index) in dado.opcionais" :key="index">{{opcional}}</li>
                        </ul>
                        </div>
                    <div>{{dado.bebida}}</div>
                    <div>{{dado.acompanhante}}</div>
                    <div id="lado">
                        <select name="status" class="status" @change="updateBurger($event, dado._id)">
                            <option value="">Seleciona</option>
                            <option v-for="statu in status" :key="statu.id" :value="statu.tipo" 
                            :selected="dado.status == statu.tipo">
                            {{statu.tipo}}
                        </option>
                        </select>
                        <button class="delete-btn" @click="deleteBurger(dado._id)">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'
import api from '../db/api'

export default {
    name: "Dashbord",
    data() {
        return {
           dados: null,
           dados_Id: null,
           status: [],
           msg: null
        }
    },
    methods: {
        async getPedidos() {
            await api
             .get("/buergers")
                .then((res) => {
                    this.dados = res.data
                })
                .catch((error) => {
                        console.log(error);
                });
           
            
            this.getStatus()
        },
        async getStatus() {
            
            await api
             .get("/status")
                .then((res) => {
                    this.status = res.data
                })
                .catch((error) => {
                        console.log(error);
                });

        },
        async deleteBurger(id) {

           await api
            .delete(`/buergers/${id}`)
            .then((res) => {
                this.getPedidos()
                console.log(res.data.msg)
                const idDelete = id.substr(21, 22)
                this.msg = `O pedido Nº ${idDelete} foi cancelado`
                setTimeout(() => this.msg = "", 3000)
            })
            .catch((error) => {
                console.log(error);
            });

           

            
        },
        async updateBurger(event, id) {

            const option = event.target.value

             await api 
             .patch(`/buergers/${id}`, {
                status: option
             })
             .then((res) => {
                const idUp = id.substr(21, 22)
                console.log(res.data)
                this.msg = `O pedido Nº ${idUp} foi atualizado para ${res.data.status}`
                setTimeout(() => this.msg = "", 3000)
             }).catch((error) => {
                console.log(error)
             })
            
        } 
    },
    mounted() {
        this.getPedidos()
    },
    components: {
        Message
    }
}
</script>

<style scoped>
    #burger-table {
        max-width: 1200px;
        margin: auto;
    }
    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    #burger-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 2px solid #ffb89a;
    }
    #burger-table-heading div,
    .burger-table-row div {
        width: 13%;
    }
    .burger-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #f8cfbe;
    }
    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
    }
    select {
        padding: 12px 6px;
        margin-right: 12px;
    }
    .delete-btn {
        background-color: #0c60b4;
        color: #f8cfbe;
        font-weight: bold;
        border: 2px solid #0c60b4;
        border-radius: 4px;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .delete-btn:hover {
        background-color: transparent;
        color: #0c60b4;
    }
    #lado {
        display: flex;
    }
</style>