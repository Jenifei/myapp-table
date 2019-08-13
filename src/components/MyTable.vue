<template>
    <div>
        <input type="text" placeholder="Please Enter..." v-model="searchText">
        <table class="gridtable">
            <thead>
                <th>OrderNumber</th>
                <th>UserName</th>
                <th>UserAge</th>
            </thead>
            <tbody>
                <tr v-for ="(item,index) in filterData" :key="(item,index)">
                    <td>{{index+1}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.age}}</td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
export default {
    name:'MyTable',
    data(){
        return{
            searchText:'',
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
            ]
        }
    },

    computed:{
        //搜索过滤
        filterData: function () {
            var searchText = this.searchText  && this.searchText.toLowerCase()
             var items = this.items
                var items1
                if (searchText) {
                    items1 = items.filter(function (item) {
                        return Object.keys(item).some(function (key) {
                            return String(item[key]).toLowerCase().match(searchText)
                        })
                    })

                } else {
                    items1 = this.items
                }
                return items1
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