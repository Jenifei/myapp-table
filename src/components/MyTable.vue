<template>
    <div>
        <input type="text" placeholder="Please Enter..." v-model="query">
        <table class="gridtable">
            <thead>
                <th>UserName</th>
                <th>UserAge</th>
            </thead>
            <tbody>
                <tr v-for ="(item,index) in showLists" :key="index">
                    <td>{{item.name}}</td>
                    <td>{{item.age}}</td>
                </tr>
                <button @click="changePage(-1)">上一页</button>
                <span>第{{showPage}}页/共{{totalPage}}页</span>
                <button @click="changePage(1)">下一页</button>
            </tbody>
        </table>

    </div>
</template>

<script>
export default {
    name:'MyTable',
    data(){
        return{
            query:'',
            item:{'name':'','age':''},
            items:[
                {'name':'Mike','age':'23'},
                {'name':'Helen','age':'21'},
                {'name':'Bob','age':'25'},
                {'name':'Nancy','age':'26'},
                {'name':'John','age':'23'},
                {'name':'Ben','age':'28'},
                {'name':'Steven','age':'22'},
                {'name':'Wendy','age':'25'},
                {'name':'Peter','age':'24'},
                {'name':'David','age':'27'},
                {'name':'Alice','age':'24'},
                {'name':'Simon','age':'21'},
                {'name':'Paul','age':'25'},
                {'name':'Rose','age':'26'},
                {'name':'Jack','age':'23'},
            ],
                totalPage:0,
                limitPage:5,
                showPage:1,
                showList:[],
                filterList:[]               
        }
    },

    mounted(){       
        this.getList();
    },

    methods:{
            getList(){
                this.showList = this.items.filter((item,index)=>{
                    if(index<this.limitPage*this.showPage && index>=this.limitPage*(this.showPage-1)){
                        return item;
                    }                  
                })
                this.getShowList();
            },
            getShowList(){
                this.showList = this.items.slice((this.showPage-1)*this.limitPage,this.showPage*this.limitPage)
                this.totalPage = Math.ceil(this.items.length/this.limitPage)
            },
            changePage(num){
                if(num === 1){
                    this.showPage++;
                    if(this.showPage>this.totalPage){
                        this.showPage = this.totalPage;

                    }
                }else if(num === -1){
                    this.showPage--;
                    if(this.showPage<=1){
                        this.showPage = 1;
                    }
                }
            this.getShowList()
        },
        listFilter(){
                var query = this.query  && this.query.toLowerCase()
                if(this.query){
                     this.filterList = this.items.filter((item)=>{
                        return Object.keys(item).some(function (key) {
                            return String(item[key]).toLowerCase().match(query)
                        })
                    })

                    this.showList = this.filterList.slice((this.showPage-1)*this.limitPage,this.showPage*this.limitPage)
                    this.totalPage = Math.ceil(this.filterList.length/this.limitPage)
                }
            }

    },
    
    computed:{
            showLists(){
                this.getShowList();
                this.listFilter();
                return this.showList;
            }
    },

}
</script>

<style scoped>
input{
    display: block;
    }
 table.gridtable {
    font-family: verdana,arial,sans-serif;
    font-size:11px;
    color:#333333;
    border-width: 1px;
    border-color: #666666;
    border-collapse: collapse;
    
}

table.gridtable th {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;
    background-color: #dedede;
}

table.gridtable td {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;
    background-color: #ffffff;
}

</style>
