<template>
    <div>
      <v-data-table
        :headers="headers"
        :items="brands"
        :options.sync="options"
        :server-items-length="totalBrands"
        :loading="loading"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td class="text-xs-center">{{props.item.id}}</td>
          <td class="text-xs-center">{{props.item.name}}</td>
          <td class="text-xs-center">{{props.item.image}}</td>
          <td class="text-xs-center">{{props.item.letter}}</td>
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
            {text: '操作', align: 'center', value: 'id', sortable: false}
          ],
          brands:[],
          options:"",
          totalBrands:3,
          loading:false,
        }
      },
      created(){
        this.brands = [
          {id:1,name:"小米",image:"",letter:"X"},
          {id:2,name:"华为",image:"",letter:"H"},
          {id:3,name:"魅族",image:"",letter:"M"},
        ]
      }

    }
</script>

<style scoped>

</style>
