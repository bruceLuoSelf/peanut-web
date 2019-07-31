<template>
    <div>
      <v-layout class="px-3 pb-0">
        <v-flex xs2>
          <v-btn  color="info">新增品牌</v-btn>
        </v-flex>
        <v-spacer/>
        <v-flex xs4>
          <v-text-field
            label="搜索"
            hide-destails append-icon="search" v-model="key"
          ></v-text-field>
        </v-flex>
      </v-layout>

      <v-data-table
        :headers="headers"
        :items="brands"
        :pagination.sync="pagination"
        :server-items-length="totalBrands"
        :loading="loading"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td class="text-xs-center">{{props.item.id}}</td>
          <td class="text-xs-center">{{props.item.name}}</td>
          <td class="text-xs-center"><img src="props.item.image" alt=""></td>
          <td class="text-xs-center">{{props.item.letter}}</td>
          <td class="text-xs-center">
            <v-btn text small color="primary">修改</v-btn>
            <v-btn text small color="error">删除</v-btn>
          </td>
        </template>
      </v-data-table>
    </div>
</template>

<script>
    export default {
      name: "MyBrand",
      data() {
        return {
          headers:[
            {text: '品牌ID', align: 'center', value: 'id'},
            {text: '名称', align: 'center', sortable: false, value: 'name'},
            {text: 'LOGO', align: 'center', sortable: false, value: 'image'},
            {text: '首字母', align: 'center', value: 'letter', sortable: true,},
            {text: '操作', align: 'center', sortable: false}
          ],
          brands:[],
          pagination:{},
          totalBrands:0,
          loading:false,
          key:""
        }
      },
      created(){
        //去后台查询
        this.loadBrands();
      },
      watch:{
        key(){
          this.loadBrands();
        },
        pagination:{
          deep:true,
          handler(){
            this.loadBrands();
          }
        }
      },
      methods:{
        loadBrands() {
          this.loading = true;
          this.$http.get("/item/brand/page", {
            params:{
              page:this.pagination.page,//当前页
              rows:this.pagination.rows,//每页大小
              sortBy:this.pagination.sortBy,//排序字段
              desc:this.pagination.descending,//是否降序
              key: this.key,//搜索条件
            }
          }).then(resp =>{

          })
          this.loading = false;
        }
      }

    }
</script>

<style scoped>

</style>
