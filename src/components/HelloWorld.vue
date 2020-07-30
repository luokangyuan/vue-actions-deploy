<template>
    <div class="hello">
        <span>用英文逗号分隔的输入数据</span>
        <input type="text" v-model="params"/>
        <button @click="getSum()" value="查询结果">查询结果</button>
        <div><span style="color: darkorange">计算结果：</span><span>{{maxSum}}</span></div>
    </div>
</template>

<script>
    export default {
        name: 'HelloWorld',
        data() {
            return {
                params: '',
                maxSum: ''
            }
        },
        methods: {
            getSum() {
                let paramsStr = this.params.split(",");
                let params = [];
                paramsStr.forEach(d => {
                    params.push(parseInt(d))
                });
                this.maxSum = this.getMaxSun(params);
            },
            getMaxSun(data) {
                if (data.length === 1) {
                    return data[0];
                }
                if (data.length === 2) {
                    return Math.max(data[0], data[1]);
                }
                if (data.length === 3) {
                    return Math.max(data[1], (data[0] + data[2]));
                }
                let s0 = data[0];
                let s1 = data[1];
                let s2 = data[0] + data[2];
                let si = 0;
                for (let i = 3; i < data.length; i++) {
                    si = data[i] + Math.max(s1, s0);
                    s0 = s1;
                    s1 = s2;
                    s2 = si;
                }
                return Math.max(si, s1);
            }
        },
        props: {
            msg: String
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
