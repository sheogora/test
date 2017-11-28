<template>  
  <div class="table-container">
    <table class="table">
      <thead>
        <th>English</th>
        <th>Translate</th>
        <th> </th>
      </thead>
      <tbody>
        <tr v-for="(row, i) in display">
          <td>{{row.english}}</td>
          <td>
            <input type="text" @change="isChanged"/>
            <!-- <input  type="text" @blur="isChanged(row)"/> -->
          </td>

        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'editable-table',
  props: {
    apiUrl: {
      type: String,
      required: true
    },
    rows: {
      type: Number,
      default: 5,
      required: false
    },
    language: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      display: []
    }
  },
  mounted() {
    this.loadData();
  },
  methods: {
    isChanged: function() {
      console.log("changed");
    },
    loadData: function() {
      var that = this;
      axios.get(this.apiUrl + "?language=" + this.language, {crossdomain:true})
      .then(response => {
        //format data 
        const list = response.data;
        var tempList = [];
        for (let i = 0; i < list.length; i++){
          let eng = list[i].en;
          let lang = list[i][that.language];
          if (!eng || !eng.file) {
            // skip broken entries
          }
          else {
            tempList.push({
              property: list[i].en.name,
              filename: (!lang || !lang.file) ? ((!eng || !eng.file) ? eng.file : "") : lang.file,
              english: eng.value,
              language: that.language,
              translation: (!lang || !lang.value) ? "" :  lang.value
            });
          }
        }
        this.display = tempList;
      })
      .catch(error => {
        console.log("error " + error);
      });
    },
    saveAll: function () {
      axios.post(this.apiUrl + "all", {crossdomain: true})
        .then(response => {
          console.log("success");
        })
        .catch(error => {
          console.log("error " + error);
        });
    }
  }
}
</script>

<style lang="scss">
</style>
