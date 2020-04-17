<template>

    <go-layout pattern="1C" class="go-page" :width="1000" :height="550">
      <go-layout-panel :searchFun="searchSubfacFun" :hasSearch="true" :searchFieldAry="acAbCtCenterDomain" cellId="a" :headerText="title" >
        <go-single-grid id="Grid1" :config="ctCenterCodeConfig" :hasPagin="true" :ref="addRefs" @selRecord="selCtCenter"> </go-single-grid>
      </go-layout-panel>
    </go-layout>

</template>

<script>
    import {mapState, mapActions} from 'vuex';

    export default {
        name: "CtCenter",
        data: function () {
            return {
              addRefs: 'addObj',
              title:'成本中心编码',
              storeName: 'AcAgShareNumStore',
            }
        },
        computed: {
            ...mapState({
              domainObj: state => state.AcAgShareNumStore.domainObj,
              domainObjSR: state => state.AcAgShareNumStore.domainObjSR,
              domainData: state => state.AcAgShareNumStore.domainData,
              domainDataSR: state => state.AcAgShareNumStore.domainDataSR,
              acAbCtCenterDomain: state => state.AcAgShareNumStore.acAbCtCenterDomain,
              ctCenterCodeConfig:state => state.AcAgShareNumStore.ctCenterCodeConfig,
            }),
        },
        methods: {
          selCtCenter(v) {
            let data = {
               ctCenterCode:v.rowRecord.ctCenterCode,
               ctCenterName:v.rowRecord.ctCenterName
            };
            this.$emit('changeMethod',data);
            GoingUtils.closeParentCurWin();
          },

          searchSubfacFun({datas}){
      //      console.log(22222,datas),
            this.$store["Grid1"].reloadData(datas)
          },
        },
        mounted() {

        },
        watch: {},
        components: {},
    }
</script>

<style scoped>
</style>
