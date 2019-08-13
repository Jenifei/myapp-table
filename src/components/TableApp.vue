<template>
    <div>
        <el-table :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)">
            <el-table-column prop="name" label="Name">
            </el-table-column>
            <el-table-column prop="age" label="Age" :sortable="true" :sort-method="sortByAge">
            </el-table-column>
        </el-table>
        <div class="block" style="margin-top:15px;">
            <el-pagination align='center' @size-change="handleSizeChange" @current-change="handleCurrentChange" :current-page="currentPage" :page-sizes="[1,5,10,20]" :page-size="pageSize" layout="total, sizes, prev, pager, next, jumper" :total="tableData.length">
            </el-pagination>
        </div>
    </div>
 
</template>

<script>
export default {
        data() {
        return {
            tableData: [
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
            currentPage: 1, 
            total: 20, 
            pageSize: 5 
        };
    },
    methods: {
        handleSizeChange(val) {
            this.currentPage = 1;
            this.pageSize = val;
        },
        handleCurrentChange(val) {
            this.currentPage = val;
        },
        //排序
        sortByDate(obj1, obj2) {
            let val1 = obj1.age
            let val2 = obj2.age
            return val1 - val2
        }
    }
}
</script>