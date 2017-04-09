<template>
  <div>
    <vuetable ref="vuetable" api-url="http://vuetable.ratiw.net/api/users"
              :fields="fields" pagination-path
              v-on:vuetable:pagination-data="onPaginationData"></vuetable>
    <!--pagination component-->
    <div class="vuetable-pagination ui basic segment grid">
      <!--pagination-info-->
      <vuetable-pagination-info ref="paginationInfo">
      </vuetable-pagination-info>
      <!--pagination-link-->
      <vuetable-pagination ref="pagination"
                           v-on:vuetable-pagination:change-page="onChangePage">
      </vuetable-pagination>
    </div>
  </div>
</template>

<script type="text/javascript">
  import accounting from 'accounting';
  import moment from 'moment';
  import Vuetable from 'vuetable-2/src/components/Vuetable';
  import VuetablePagination from 'vuetable-2/src/components/VuetablePagination';
  import VuetablePaginationInfo from 'vuetable-2/src/components/VuetablePaginationInfo';
  import CustomActions from './CustomActions';
  import Vue from 'vue';

  Vue.component('custom-actions', CustomActions);

  export default {
    components: {
      Vuetable,
      VuetablePagination,
      VuetablePaginationInfo,
    },
    data(){
      return {
        fields: [
          {
            name: '__checkbox',
            title: '#',
            titleClass: 'center aligned',
            dataClass: 'center aligned'
          },
          {
            name: 'name',
            sortField: 'name'
          },
          {
            name: 'email',
            sortField: 'email'
          },
          {
            name: 'age',
            sortField: 'birthdate',
            dataClass: 'center aligned'
          },
          {
            name: 'birthdate',
            titleClass: 'center aligned',
            dataClass: 'center aligned',
          },
          {
            name: 'nickname',
            callback: 'allcap'
          },
          {
            name: 'gender',
            titleClass: 'center aligned',
            dataClass: 'center aligned'
          },
          {
            name: 'salary',
            titleClass: 'center aligned',
            dataClass: 'center aligned',
            visible: false
          },
          {
            name: '__component:custom-actions',
            title: 'Actions',
            titleClass: 'center aligned',
            dataClass: 'center aligned'
          }
        ]
      }
    },
    methods: {
      allcap(value){
        return value.toUpperCase();
      },
      onPaginationData(paginationData){
//        debugger;
        this.$refs.pagination.setPaginationData(paginationData);
        this.$refs.paginationInfo.setPaginationData(paginationData);
      },
      onChangePage(page){
//        debugger;
        this.$refs.vuetable.changePage(page);
      }
    }
  }
</script>

<style>

</style>
