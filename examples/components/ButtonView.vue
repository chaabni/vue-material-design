<template>
  <div>
    <page-header :title="title" :description="description"></page-header>
    <example :code-html="html" class="button-examples">
      <base-button label="BUTTON" slot="ex" ></base-button>
      <base-button label="FACEBOOK" slot="ex" :label-style="labelStyle" background-color="rgb(58, 87, 149)" :shadow-depth='1' icon-class="fa fa-facebook-official fa-2x"></base-button>
      <base-button label="LINUX" slot="ex" :label-style="labelStyle" background-color="rgb(73, 219, 114)" :shadow-depth='1' :is-icon-front=true icon-class="fa fa-linux fa-2x"></base-button>
      <base-button label="GITHUB LINK" slot="ex" :shadow-depth=1 link='https://github.com' icon-class="fa fa-github fa-2x"></base-button>
      <base-button label="FLOAT BUTTON" slot="ex" :shadow-depth=1 :is-float="true"></base-button>
      <base-button label="DISABELED" slot="ex" :disabled="true"></base-button>
    </example>
    <property>
      <table-wrapper slot="pro">
        <table-header slot="header" :headers="tableHeader"></table-header>
        <table-body slot="body" :body-content="bodyContent" class="desc"></table-body>
      </table-wrapper>
    </property>
  </div>
</template>

<script type="text/javascript">
import PageHeader from 'PageHeader'
import Example from 'Example'
import Property from 'Property'
import desc from '../helpers/property'
import {BaseButton, TableWrapper,TableBody, TableHeader} from 'material-vue'

export default {
  data: function() {
    return {
      title: 'Buttons',
      description: 'A button clearly communicates what action will occur when the user touches it.',
      tableHeader: ['property','type','default','description'],
      bodyContent: desc.button,
      labelStyle: {
        color: '#eff2f4'
      },
      html: '<base-button label="BUTTON"></base-button> \
              \n<base-button label="FACEBOOK" background-color="rgb(58, 87, 149)" :shadow-depth="1" icon-class="fa fa-facebook-official fa-2x"></base-button> \
              \n<base-button label="LINUX" background-color="rgb(73, 219, 114)" :shadow-depth="1" :is-icon-front=true icon-class="fa fa-linux fa-2x"></base-button> \
              \n<base-button label="GITHUB LINK" :shadow-depth=1 link="https://github.com" icon-class="fa fa-github fa-2x"></base-button> \
              \n<base-button label="FLOAT BUTTON" :shadow-depth=1 :is-float=true></base-button> \
              \n<base-button label="DISABELED" :disabled=true></base-button>'
    }
  },
  components: {
    PageHeader,
    Example,
    Property,
    BaseButton,
    TableBody,
    TableHeader,
    TableWrapper
  }
}
</script>
<style media="screen" lang="scss">
@import "../styles/common.scss";
.button-examples {
  [slot="ex"] {
    margin: 10px !important;
  }
}

</style>
