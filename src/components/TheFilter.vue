<template>
 <div role="tablist" class="thefilter">
   <b-card no-body class="mb-1 small" v-for="item in items" :key="item.id">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-btn block href="#" v-b-toggle="item.collapseId" variant="primary" size="sm">{{ item.collapseName }}</b-btn>
      </b-card-header> 
      <b-collapse :id="item.collapseId" visible role="tabpanel"> 
        <!-- accordion="my-accordion" removed to let b-card opened when clicking another one -->
        <b-card-body class="p-0">
          <b-table :fields="fields" :items="item.params" thead-class="hide_header">
            <template slot="inp" slot-scope="data">
              
              <div :is="item.params[data.index].controll" :value.sync="item.params[data.index].val" :options = "item.params[data.index].SelectOptions"></div>
              <!-- :value.sync - two-way binding” for a prop value passed to controll -->
              <!-- item.params[data.index].controll - you can add any controll using slot, set the type of contoll in itmes array  - -->
              {{ item.params[data.index].val }}
            </template>
            <template slot="combobox" slot-scope="data">
              <b-select v-model="item.params[data.index].selected" :options="combobox_items" class="form-control-sm"></b-select>              
               {{ item.params[data.index].selected }} 
            </template>           
          </b-table>
        </b-card-body>
      </b-collapse>
    </b-card>


  </div>
</template>

<script>

import BaseBtn from './BaseBtn.vue'
import BaseInp from './BaseInp.vue'
import BaseSelect from './BaseSelect.vue'

export default {
  components: { BaseBtn, BaseInp, BaseSelect },
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      selectedvalue: 0,
      testval: 'new',
      items:
        [{"collapseId": "1",
        "collapseName": "Объект учета",        
        "params": [
          { "selected": '%', "dbfield": "RNO_NUM", "name": "Реестровый номер", "controll": "BaseInp", "SelectOptions": "", "val": "", },
          { "selected": '%', "dbfield": "ISKL", "name": "Исключен", "controll": "BaseSelect", "SelectOptions": [{value: 1, text: 'Исключен'},{value: 2, text: 'Не исключен'}], "val": "test" },
          { "selected": '%', "dbfield": "TTT", "name": "Свободен", "controll": "BaseInp", "SelectOptions": "", "val": "" },
          { "selected": '%', "dbfield": "RNO_LOA_ID", "name": "Тип", "controll": "BaseInp", "SelectOptions": "", "val": "" }]
        },
        {"collapseId": "2",
        "collapseName": "Свидетельство",
        "params": [
          { "selected": '', "dbfield": "RNO_NUM", "name": "Реестровый номер", "controll": "BaseInp", "val": "" },
          { "selected": '', "dbfield": "ISKL", "name": "Исключен", "controll": "BaseInp", "val": "" },
          { "selected": '', "dbfield": "TTT", "name": "Свободен", "controll": "BaseInp", "val": "" },
          { "selected": '', "dbfield": "RNO_LOA_ID", "name": "Тип", "controll": "BaseInp", "val": "" }]
        }],
      combobox_items: [
        { value: "%", text: 'Содержит' },
        { value: "=", text: 'Равно' },
        { value: ">", text: 'Больше' },
        { value: "<", text: 'Меньше' }
      ],
      select_options: [
        {value: 1, text: 'Исключен'},
        {value: 2, text: 'Не исключен'}
      ],
          fields: [
         { key: 'name', label: 'name',  },
         { key: 'combobox', label: 'combobox' },
         { key: 'inp', label: 'inp' }
        //  { key: 'btn', label: 'btn' }
       ]
    }
  }
  ,methods: {
      change: function(value) {
      this.testval = value;
      }
  }
}
</script>


<style scoped>
.thefilter {  
  width: 500px;
}
.ttt{
  float: right;
}
</style>

