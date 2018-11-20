<template>
    <div>
        <input v-model="entrada">
        <button @click="adicionarLista">Adicionar Lista</button>
        <lista
            v-for="lista in listas"
            :key="lista.id"
            :lista="lista"
            @itemAdicionado="adicionarItem"
        ></lista>
    </div>
</template>

<script>
import Lista from "@/components/Lista";

export default {
    components: {
        Lista
    },

    data() {
        return {
            entrada: "",
            listas: []
        };
    },

    methods: {
        adicionarLista() {
            const novaLista = {
                id: this.listas.length + 1,
                nome: this.entrada,
                itens: []
            };
            this.listas.push(novaLista);
            this.entrada = "";
        },

        adicionarItem(novoItem, idLista) {
            const lista = this.listas.find(lista => lista.id === idLista);
            lista.itens.push(novoItem);
        }
    }
};
</script>