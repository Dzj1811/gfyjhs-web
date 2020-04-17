<template>

    <go-layout pattern="1C" class="go-page" :width="1000" :height="550">
      <go-layout-panel :searchFun="searchSubfacFun" :hasSearch="true" :searchFieldAry="AcAbSubfacDomain" cellId="a" :headerText="title" >
        <go-single-grid id="subfac_Grid" :config="subfacConfig" :hasPagin="true" :ref="addRefs" @selRecord="selSubfac"> </go-single-grid>
      </go-layout-panel>
    </go-layout>

</template>

<script>
    import {mapState, mapActions} from 'vuex';

    export default {
        name: "Subfac",
        data: function () {
            return {
              addRefs: 'addObj',
              title:'成本要素编码',
              storeName: 'AcAgSubfacMaterialStore',
            }
        },
        computed: {
            ...mapState({
              domainObj: state => state.AcAgSubfacMaterialStore.domainObj,
              domainObjSR: state => state.AcAgSubfacMaterialStore.domainObjSR,
              domainData: state => state.AcAgSubfacMaterialStore.domainData,
              domainDataSR: state => state.AcAgSubfacMaterialStore.domainDataSR,
              AcAbSubfacDomain: state => state.AcAgSubfacMaterialStore.AcAbSubfacDomain,
              subfacConfig:state => state.AcAgSubfacMaterialStore.subfacConfig,
           //   domainData:state => state.AcAgSubfacMaterialStore.domainData,
            }),
        },
        methods: {
          selSubfac(v) {
            let data = {
              subfacCode: v.rowRecord.subfacCode,
              subfacName:v.rowRecord.subfacName
            };

            this.$emit('changeMethod',data);
            GoingUtils.closeParentCurWin();
          },
         /* searchSubfacFun({datas}) {
            this.$refs.addObj.reloadData(datas);
          },*/
          searchSubfacFun({datas}){
            this.$store["subfac_Grid"].reloadData(datas)
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
