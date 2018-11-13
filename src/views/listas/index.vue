<template>
    <div id="listas">
        <h1> Minhas listas!</h1>
        <section>
            <input v-model="novaListaNome" placeholder="Nome da Lista">
            <button @click="adicionarLista">Adicionar Lista</button>
        </section>
        <section v-for="lista in listas" :key="lista.id">
            <h3>{{ lista.nome }}</h3>
            <button @click="() => removerLista(lista.id)">Remover Lista</button>
            <ul>
                <li v-for="item in lista.itens" :key="item.id">
                    {{ item.id + ". " + item.descricao }}
                    <input type="checkbox" v-model="item.status">
                    {{ item.status ? "OK" : "NOPE" }}
                    <button @click="() => removerItem(lista.id, item.id)">Remover</button>
                </li>
            </ul>
            <input v-model="lista.novoItem.descricao" placeholder="Descrição">
            <br>
            <button @click="() => salvarItem(lista.id)">Salvar</button>
        </section>
    </div>
</template>

<script>
export default {
    name: "listas",

    data() {
        return {
            novaListaNome: "",
            listas: []
        }
    },

    methods: {
        salvarItem(idLista) {
            const posicao = this.listas.findIndex(lista => lista.id === idLista);
            if (this.listas[posicao].novoItem.descricao === "") return;
            const novoItem = {
                id: this.listas[posicao].itens.length + 1,
                descricao: this.listas[posicao].novoItem.descricao,
                status: false,
            }
            this.listas[posicao].itens.push(novoItem);
            this.listas[posicao].novoItem.descricao = "";
        },

        removerItem(idLista, idItem) {
            const posicaoLista = this.listas.findIndex(lista => lista.id === idLista);
            const posicaoItem = this.listas[posicaoLista].itens.findIndex(item => item.id === idItem);
            this.listas[posicaoLista].itens.splice(posicaoItem, 1);
        },

        adicionarLista() {
            if (this.novaListaNome === "") return;
            const novaLista = {
                id: this.listas.length + 1,
                nome: this.novaListaNome,
                itens: [],
                novoItem: {
                    descricao: ""
                }
            }
            this.listas.push(novaLista);
            this.novaListaNome = "";
        },

        removerLista(idLista) {
            const posicaoLista = this.listas.findIndex(lista => lista.id === idLista);
            this.listas.splice(posicaoLista, 1);
        }
    }
}
</script>

<style scoped>
    section {
        max-width: 300px;
        border: 1px solid;
        text-align: center;
    }
</style>