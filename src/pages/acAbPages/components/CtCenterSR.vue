<template>

    <go-layout pattern="1C" class="go-page" :width="1000" :height="550">
      <go-layout-panel :searchFun="searchCtCenterFun" :hasSearch="true" :searchFieldAry="acAbCtCenterDomain" cellId="a" :headerText="title" >
        <go-single-grid id="ct_service_center_Grid" :config="ctCenterCodeConfig" :hasPagin="true" :ref="addRefs" @selRecord="selCtCenterSR"> </go-single-grid>
      </go-layout-panel>
    </go-layout>

</template>

<script>
    import {mapState, mapActions} from 'vuex';

    export default {
        name: "CtCenterSR",
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
          selCtCenterSR(v) {
            let data = {
              ctCenterCode:v.rowRecord.ctCenterCode,
              ctCenterName:v.rowRecord.ctCenterName
            };
            this.$emit('changeMethod',data);
            GoingUtils.closeParentCurWin();
          },
         /* searchSubfacFun({datas}) {
            this.$refs.addObj.reloadData(datas);
          },*/
          searchCtCenterFun({datas}){
            this.$store["ct_service_center_Grid"].flushGridByUrl({ url: "/gfyjhs-server/acAbCtCenter/readAllData/"+StorageUtils.getSessionItem('accountId'),params:datas});
            //this.$store["Grid"].reloadData(datas)
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
