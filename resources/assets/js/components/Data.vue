<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-12">
                <div class="panel panel-default">
                    <h3 class="panel-heading">初任人員平均經常性薪資</h3>
​
                    <div class="panel-body">
                        <table class="table-condensed data-table">
                            <thead>
                                <tr>
                                    <th v-if="dataset.resultData.length>0" v-for="(title,titleKey) in dataset.resultDataKey" :key="titleKey">{{ title }}</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-if="dataset.resultData.length>0" v-for="(data,dataKey) in dataset.resultData" :key="dataKey">
                                    <td v-if="dataset.resultData.length>0" v-for="(subData,subDataKey) in data" :key="subDataKey">{{ subData }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
​
<script>
    export default {
        created(){
            this.init();
        },
        data(){
            return{
                dataset:{
                    resultData:[],
                    resultDataKey:[]
                }
            }
        },
        methods:{
            init(){
                let self = this;
                axios({
                    method: 'post',
                    url: '/Datas',
                })
                    .then(function(response){
                        if(response.data.success==true){
                            let resultData = response.data.result.records;
                            self.dataset.resultData = resultData;
                            //集合陣列的key
                            for(let i=0; i<resultData.length; i++){
                                self.dataset.resultDataKey = Object.keys(resultData[i]);
                            }
                        }
                    })
            }
        }
    }
</script>