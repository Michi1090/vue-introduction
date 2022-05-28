<template>
    <div id="app">
        <Calc :title="message" v-on:result-event="appAction"></Calc>
        <div class="mt-3 text-left">
            <table class="table" v-html="log"></table>
        </div>
        <div>
            <button class="btn btn-danger" v-on:click="doClear">
                Clear Log
            </button>
        </div>
    </div>
</template>

<script>
import Calc from './components/Calc.vue'

export default {
    name: 'App',
    components: {
        Calc
    },
    data() {
        return {
            message: 'CALC',
            result: [],
        }
    },
    computed: {
        log() {
            let table =
                /* html */
                `<tr><th>Expression</th><th>Value</th></tr>`;

            if (this.result.length > 0) {
                for (let i in this.result) {
                    table +=
                        /* html */
                        `<tr>
                            <td>${this.result[i][0]}</td>
                            <td>${this.result[i][1]}</td>
                        </tr>`;
                }
            }

            return table
        }
    },
    created() {
        let items = localStorage.getItem('log');
        let logs = JSON.parse(items);

        if (logs != null) {
            this.result = logs;
        }
    },
    methods: {
        appAction(exp, res) {
            console.log(exp, res)
            this.result.unshift([exp, res]);
            let log = JSON.stringify(this.result);
            console.log(log)
            localStorage.setItem('log', log);
        },
        doClear() {
            if (confirm('ログをすべて消去します')) {
                localStorage.removeItem('log');
                this.result = [];
            }
        }
    }
}
</script>
