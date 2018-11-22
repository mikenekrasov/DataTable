<template>
    <table>
        <thead>
            <tr>
            <th v-for="col in columns">{{col}}</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="row in filtered" :class = "{ 'selected': clicked }" @click="toggle(clicked)">
            <td v-for="col in columns">{{row[col]}}</td>
            </tr>
        </tbody>     
    </table>
</template>
<script>
export default {
    name: "data-table",
    props:{
        rows: Array,
        filter: String,
    },
    data(){
        return {
            clicked: false
        }
    },
    computed: {
        columns() {
          if (this.rows.length == 0) {
            return [];
          }
            return Object.keys(this.rows[0]).filter(function(key) {
                //return key !== 'id'
                return ["id"].indexOf(key) === -1;
            }
        );
        },
        filtered(filter) {
            var filter = this.filter && this.filter.toLowerCase();
          var data = this.rows;
          if (filter) {
              data = data.filter(function (row) {
                return Object.keys(row).some(function (key) {
                  return String(row[key]).toLowerCase().indexOf(filter) > -1
                })
              })
              return data;
        }else{
            return data;
        }
        }
    },
    methods: {
        toggle(clicked) {
                clicked = !clicked
            }
    }
}
</script>
<style>
    table {
  font-family: 'Open Sans', sans-serif;
  width: 750px;
  border-collapse: collapse;
  border: 3px solid #44475C;
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  text-align: left;
  background: #44475C;
  color: #FFF;
  padding: 8px;
  min-width: 30px;
}

table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
  border-bottom: 2px solid #7D82AB;
}
table td:last-child {
  border-right: none;
}
/* table tbody tr:nth-child(2n) td {
  background: #FFFFFF;
} */
table tr{
    cursor: pointer;
}
.selected {
    background: red;
}
</style>
