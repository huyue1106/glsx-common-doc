<template>
  <div>
    <gl-table :table="constsData"></gl-table>
  </div>
</template>

<script>
export default {
  name: 'consts',
  data () {
    return {
      constsData: {
        border: true,
        // export: true,
        // height: parseInt(window.screen.height - 450),
        align: 'center',
        data: [{}],
        column: [{
          label: 'Key',
          prop: 'Key'
        }, {
          label: '描述',
          prop: 'description'
        }]
      }
    }
  },
  mounted () {
    this.$http.get('../../static/data.json').then(res => {
      this.constsData.data = res.body.consts
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
