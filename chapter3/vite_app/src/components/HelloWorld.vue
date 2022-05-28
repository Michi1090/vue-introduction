<template>
    <div class="alert alert-info">
        <h2>{{ title }}</h2>
        <p ref="msg">{{ message }}</p>
        <hr>
        <div>
            <button class="btn btn-info mt-2" v-on:click="doAction">Click</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data() {
        return {
            title: 'Hello World',
            message: 'This is sample message.',
        }
    },
    mounted() {
        this.counter = 0
    },
    methods: {
        doAction() {
            this.counter++
            this.$refs.msg.innerHTML +=
            /* html */
            `<h6>counted: ${this.counter}</h6>`
        }
    }
}
</script>
