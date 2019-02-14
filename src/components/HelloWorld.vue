<template>
    <div class="hello">
        <div>
            <p>信息录入:</p>
            <table border="1">
                <tr>
                    <th>序号</th>
                    <th>单价</th>
                    <th>数量</th>
                    <th>金额</th>
                    <th>操作</th>
                </tr>
                <tr v-for="(item,index) in dataInput" :key="index">
                    <td>{{ index + 1 }}</td>
                    <td><input :value="item.price" @change="changePrice(index,$event)"></td>
                    <td><input :value="item.amount" @[inputEvent]="changeAmount(index,$event)"></td>
                    <td><input :value="item.total" @[inputEvent]="changeTotal(index,$event)"></td>
                    <td><span class="operator" @click="addOne(index)">+</span> <span class="operator" @click="removeThis(index)">-</span></td>
                </tr>
            </table>
        </div>
        <div>
            <p>信息重置:<a href="javascript:;" @click="setCurrentData()">重置数据</a></p>
            <table border="1">
                <tr>
                    <th>序号</th>
                    <th>单价</th>
                    <th>数量</th>
                    <th>金额</th>
                    <th>操作</th>
                </tr>
                <tr v-for="(item,index) in dataReset" :key="index">
                    <td>{{ index + 1 }}</td>
                    <td><input :value="item.price" @change="changePrice(index,$event)"></td>
                    <td><input :value="item.amount" @[inputEvent]="changeAmount(index,$event)"></td>
                    <td><input :value="item.total" @[inputEvent]="changeTotal(index,$event)"></td>
                    <td><span class="operator" @click="addOne(index)">+</span> <span class="operator" @click="removeThis(index)">-</span></td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>

    const initData = [{}];

    export default {
        name: 'HelloWorld',
        data: function () {
            return {
                inputEvent:'change',
                dataInput: initData,
                dataReset: initData
            };
        },
        methods:{
            changePrice(index,event){
                let currentData = this.dataInput[index];
                this.$set(currentData,'price',event.target.value)
                this.$set(currentData,'total',currentData.price * currentData.amount)
            },
            changeAmount(index,event){
                let currentData = this.dataInput[index];
                this.$set(currentData,'amount',event.target.value)
                this.$set(currentData,'total',currentData.price * currentData.amount)
            },
            changeTotal(index,event){
                let currentData = this.dataInput[index];
                this.$set(currentData,'total',event.target.value)
                this.$set(currentData,'price',currentData.total / currentData.amount)
            },
            addOne(index){
                this.dataInput.splice(index + 1,0,{})
            },
            removeThis(index){
                this.dataInput.splice(index,1)
            },
            setCurrentData(data){
                this.dataReset = data || [{price:1,amount:2},{
                    price:2,
                    total:4
                }];
                this.dataInput = this.dataReset;
            }
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

    .operator{
        cursor:pointer;
        margin:0 10px;
    }
</style>
