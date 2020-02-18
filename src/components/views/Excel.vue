<template lang="html">
  <div class="wrapper-jexcel">
    <div class="introduction"><span>Data Mahasiswa</span></div>
    <input
      type="button"
      value="Add new row"
      @click="jExcelObj.insertRow()"
    /><br />
    <div id="spreadsheet" ref="spreadsheet"></div>
  </div>
</template>

<script>
import jexcelStyle from 'jexcel/dist/jexcel.css' // eslint-disable-line no-unused-vars
import jexcel from 'jexcel' // eslint-disable-line no-unused-vars

export default {
  name: 'jexcel',
  data() {
    return {
      mahasiswa: [
        [
          '05111740000084', 'Fachry', '2017'
        ]
      ]
    }
  },
  computed: {
    jExcelOptions() {
      return {
        data: this.mahasiswa,
        columns: [
          { type: 'text', title: 'NRP', width: '150px' },
          { type: 'text', title: 'Nama', width: '200px' },
          { type: 'dropdown', title: 'Angkatan', width: '150px', source: ['2014', '2015', '2016', '2017', '2018'] },
          { type: 'calendar', title: 'Tanggal Lahir', width: '150px' },
          { type: 'image', title: 'Photo', width: '200px' },
          { type: 'checkbox', title: 'Aktif', width: '50px' }
        ]
      }
    }
  },
  methods: {
    insertRowc() {
      console.log(this)
      // this.spreadsheet.insertRow();
    }
  },
  mounted: function() {
    // console.log(this.jExcelOptions);
    // console.log(this.$refs["spreadsheet"]);
    const jExcelObj = jexcel(this.$refs['spreadsheet'], this.jExcelOptions)
    // Object.assign(this, jExcelObj); // pollutes component instance
    Object.assign(this, { jExcelObj })// tucks all methods under jExcelObj object in component instance
    // console.log(this.jExcelObj);
  }
}
</script>

<style lang="css" scoped>
.introduction {
  font-size: 50px;
  text-align: center;
  padding: 0.5em;
  margin-bottom: 0.3em;
  color: black;
}
</style>
