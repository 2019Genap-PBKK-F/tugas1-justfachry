<template>
  <div class="wrapper-jexcel">
      <h1 style="text-align:center">Data Mahasiswa</h1>
    <input type="button" value="Add new row" @click="jExcelObj.insertRow()"/>
    <input type="button" value="Delete Row" @click="jExcelObj.deleteRow()"/>
    <br />
    <div id="spreadsheet" ref="spreadsheet"></div>
  </div>
</template>

<script>
import jexcelStyle from 'jexcel/dist/jexcel.css' // eslint-disable-line no-unused-vars
import jexcel from 'jexcel' // eslint-disable-line no-unused-vars
import axios from 'axios'

export default {
  name: 'jexcel',
  data() {
    return {
      mahasiswa: [],
      form: { id: '', nrp: '', nama: '', angkatan: '', tanggal: '', photo: '', aktif: ''
      }
    }
  },
  computed: {
    jExcelOptions() {
      return {
        url: 'http://localhost:3000/mahasiswa/',
        data: this.mahasiswa,
        allowToolbar: true,
        onchange: this.updateRow,
        oninsertrow: this.newRow,
        ondeleterow: this.deleteRow,
        columns: [
          { type: 'hidden', title: 'id' },
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
    newRow() {
      axios.post('http://localhost:3000/mahasiswa/', this.form).then(res => {
        console.log(res.data)
      })
    },
    updateRow(instance, cell, columns, row, value) {
      axios.get('http://localhost:3000/mahasiswa/' + (parseInt(row) + 1)).then(res => {
        var index = Object.values(res.data)
        index[columns] = value
        console.log(index)
        axios.put('http://localhost:3000/mahasiswa/' + index[0], {
          id: index[0],
          nrp: index[1],
          nama: index[2],
          angkatan: index[3],
          tanggal: index[4],
          photo: index[5],
          aktif: index[6]
        }).then(res => {
          console.log(res.data)
        })
      })
    },
    deleteRow(instance, row) {
      axios.get('http://localhost:3000/mahasiswa/').then(res => {
        var index = Object.values(res.data[row])
        console.log(row)
        axios.delete('http://localhost:3000/mahasiswa/' + index[0])
      })
    }
  },
  mounted: function() {
    const jExcelObj = jexcel(this.$refs['spreadsheet'], this.jExcelOptions)
    Object.assign(this, { jExcelObj })
  }
}
</script>
