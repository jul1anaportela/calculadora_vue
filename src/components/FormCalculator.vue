<script setup>
const props = defineProps(['calculateResult', 'number1', 'number2', 'operation', 'getOperationSymbol', 'result'])
</script>

<template>
    <form @submit.prevent="props.calculateResult">
        <div class="row">
            <div class="col-md-2">
                <input type="number" class="form-control" v-model="props.number1">
            </div>
            <div class="col-md-2">
                <select class="form-control" v-model="props.operation">
                    <option value="select">select</option>
                    <option value="sum">+</option>
                    <option value="subtract">-</option>
                    <option value="division">:</option>
                    <option value="multiply">x</option>
                </select>
            </div>
            <div class="col-md-2">
                <input type="number" class="form-control" v-model="props.number2">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">result</button>
            </div>
        </div>
        <div class="row mt-5">
            <h4>Result:</h4>
            <span>{{ previousNumber1 }} {{ props.getOperationSymbol(props.operation) }} {{ previousNumber2 }} = {{
        props.result !== null ? props.result : '' }}</span>
        </div>
    </form>
</template>