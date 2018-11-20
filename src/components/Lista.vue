<template>
    <div class="lista">
        <h3>{{ lista.id }}. {{ lista.nome }}</h3>
        <ul>
            <li v-for="item in lista.itens" :key="item.id">
                {{ item.id }}. {{ item.descricao }}
                <input type="checkbox" v-model="item.status">
            </li>
        </ul>
        <input v-model="entrada">
        <button @click="adicionarItem">Adicionar Item</button>
    </div>
</template>

<script>
export default {
    props: ["lista"],

    data() {
        return {
            entrada: ""
        };
    },

    methods: {
        adicionarItem() {
            const novoItem = {
                id: this.lista.itens.length + 1,
                descricao: this.entrada,
                status: false
            };
            this.$emit("itemAdicionado", novoItem, this.lista.id);
        }
    }
};
</script>

<style scoped>
.lista {
    border-collapse: collapse;
    border: 1px solid;
}
</style>