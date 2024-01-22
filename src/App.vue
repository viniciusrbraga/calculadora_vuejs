<script setup>
import { reactive } from 'vue';

const estado = reactive({
    numero1: 0,
    numero2: 0,
    operacao: ''
})

function soma() {
    const { numero1, numero2 } = estado
    return parseFloat(numero1) + parseFloat(numero2);
}

function subtrai() {
    const { numero1, numero2 } = estado
    return parseFloat(numero1) - parseFloat(numero2);
}

function mnultiplica() {
    const { numero1, numero2 } = estado
    return parseFloat(numero1) * parseFloat(numero2);
}

function divide() {
    const { numero1, numero2 } = estado
    return (numero2 != 0 ? (parseFloat(numero1) / parseFloat(numero2)) : "Divisão por ZERO não é permitida");
}

const executa = () => {
    const { operacao } = estado;
    switch (operacao) {
        case '+':
            return soma();
        case '-':
            return subtrai();
        case '*':
            return mnultiplica();
        case '/':
            return divide();
        default:
            return 'Selecione uma operação';
    }
} 
</script>

<template>
    <div class="container">
        <h1 class="mt-4 mb-6">Calculadora</h1>
        <span>Informe 2 números</span> <br>

        <input type="number" @keyup="evento => estado.numero1 = evento.target.value" placeholder="Primeiro valor"
            class="mb-2" > <br> 

        <input type="number" @keyup="evento => estado.numero2 = evento.target.value" placeholder="Segundo valor"
            class="mb-2"> <br>

        <select @change="evento => estado.operacao = evento.target.value" class="form-control mb-2">
            <option value="" disabled selected hidden>Operação</option>
            <option value="+">+</option>
            <option value="-">-</option>
            <option value="*">*</option>
            <option value="/">/</option>
        </select>

        Resultado ={{ executa() }}

    </div>
</template>

<style scoped>
select {
    max-width: 195px;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
}

input[type=number] {
    -moz-appearance: textfield;
}
</style>