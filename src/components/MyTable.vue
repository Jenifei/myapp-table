<template>
    <div>
        <input type="text" placeholder="Please Enter..." v-model="query">
        <table class="gridtable">
            <thead>
                <th>UserName</th>                         
                <th >UserAge<span @click="sort('age')"><a> ↑↓</a></span></th>
            </thead>
            <tbody>
                <tr v-for ="(item,index) in showLists" :key="index">
                    <td>{{item.name}}</td>
                    <td>{{item.age}}</td>
                </tr>
            </tbody>
            <button @click="prevPage">上一页</button>
            <span>第{{currentPage}}页/共{{totalPage}}页</span>
            <button @click="nextPage">下一页</button>
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
            currentSort:'name',
            currentSortDir:'asc',
            totalPage:0,
            pageSize:5,
            currentPage:1
        }
    },

    mounted(){  
        this.totalPage=Math.ceil(this.items.length/this.pageSize);
        this.totalPage=this.totalPage==0?1:this.totalPage; 
    },

    methods:{
        sort:function(s) {
            if(s === this.currentSort) {
                this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
            }
            this.currentSort = s;
        },
        nextPage:function() {
            if((this.currentPage*this.pageSize) < this.items.length) this.currentPage++;
        },
        prevPage:function() {
            if(this.currentPage > 1) this.currentPage--;
        }
    },
    
    computed:{
        showLists:function() {
            var items = this.items
            var query = this.query  && this.query.toLowerCase()
            return items.sort((a,b) => {
                let modifier = 1;
                if(this.currentSortDir === 'desc') modifier = -1;
                if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
                if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
                return 0;
            }).filter((item, index) => {
                let start = (this.currentPage-1)*this.pageSize;
                let end = this.currentPage*this.pageSize;
                if(index >= start && index < end){
                    return Object.keys(item).some(function (key) {
                        return String(item[key]).toLowerCase().match(query)
                    })
                }
            });
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
a:hover{
    cursor:pointer
}
</style>
