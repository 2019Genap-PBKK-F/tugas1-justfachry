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
          'Fachry'
        ]
      ]
    }
  },
  computed: {
    jExcelOptions() {
      return {
        data: this.mahasiswa,
        columns: [
          { type: 'text', title: 'Nama', width: '120px' }
        //   {
        //     type: "dropdown",
        //     title: "Make",
        //     width: "250px",
        //     source: ["Alfa Romeo", "Audi", "BMW", "Honda", "Porshe"]
        //   },
        //   { type: "calendar", title: "Available", width: "250px" },
        //   { type: "image", title: "Photo", width: "120px" },
        //   { type: "checkbox", title: "Stock", width: "80px" },
        //   {
        //     type: "numeric",
        //     title: "Price",
        //     width: "120px",
        //     mask: "$ #.##,00",
        //     decimal: ","
        //   },
        //   { type: "color", width: "100px", render: "square" }
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
  font-size: 14px;
  padding: 0.5em;
  margin-bottom: 0.3em;
  color: gold;
  background: #111;
}
</style>
