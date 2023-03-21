<template>
<div id="app">
  <div class="body">
  <h2>Exploratory Dashboard</h2>
  <center><p>This is a sample page for ihr covid19.Just showing the graph according to the corresponding data.You should give the source and timeperiod to show the graph.Graph is according to the given source and timeperiod.You can check the important source of the country on Network selector button.Graph is shown on the buttom.</p></center>
  <div class="inputs">
  <div class="q-pa-md" style="max-width:300px"  >
    <div class="q-gutter-md ">
      <form>
          <div class="userbox">
      <q-select outlined v-model="modeld" :options="destinationoptions" label="destination" />
      </div>
      <div class="q-pa-md" style="padding-left: 20%;position: absolute;">
    <q-btn class="hintbtn" color="primary" push label="Network Selector">
      <q-popup-proxy>
        <q-banner v-if="modeld==null">
          Select any destination
        </q-banner>
        <q-banner v-if="modeld=='India'">
          Select the following ASN for India
          <ul>
            <li>AS55836 Reliance Jio Limited</li>
            <li>AS45609 Bharti Airtel Ltd</li>
          </ul>
        </q-banner>
        <q-banner v-if="modeld=='Japan'">
          Select the following ASN for Japan
          <ul>
            <li>AS2516 KDDI KDDI CORPORATION</li>
            <li>AS17676 GIGAINFRA Softbank BB Corp</li>
            <li>AS4713 OCN NTT Communications</li>
          </ul>
        </q-banner>
        <!-- <q-banner v-if="modeld=='France'">
          Select the following ASN for France
          <ul>
            <li>AS3215 Orange S.A.</li>
            <li>AS12322 PROXAD Free SAS</li>
            <li>AS15557 LDCOMNET SFR SA</li>
            <li>AS5410 Bouygues Telecom SA</li>
          </ul>
        </q-banner> -->
        <q-banner v-if="modeld=='Ukraine'">
          Select the following ASN for Ukraine
          <ul>
            <li>AS15895 KSNET "Kyivstar"</li>
            <li>AS21497 UMC-AS</li>
            <li>AS6849 UKRTELNET "Ukrtelecom"</li>
          </ul>
        </q-banner>
        <q-banner v-if="modeld=='United Arab Emirates'">
          Select the following ASN for United Arab Emirates
          <ul>
            <li>AS5384 Emirates Telecommunications</li>
            <li>AS15802 DU Emirates Integrated</li>
          </ul>
        </q-banner>
      </q-popup-proxy>
    </q-btn>
  </div>
      
      <div class="userbox">
      <q-select outlined v-model="models" :options="sourceoptions" label="source" />
      </div>
      <div class="userbox">
      <q-select outlined v-model="modelt" :options="timeperiodoptions" label="timeperiod" />
      </div>
      <div class="userbox">
      <q-select outlined v-model="modelm" :options="metricsoptions" label="metrics" />
      </div>
      <center class="btns">
      <q-btn @click="submit" outline rounded label="Submit" />
      <h6><a href="https://ihr.iijlab.net/ihr/en-us/covid19">Check the reference on ihr</a></h6>
      </center>
      </form>
    </div>
  </div>
  </div>
  </div>
  </div>
  
  <div class="q-pa-md q-gutter-sm" style="padding-left: 20%;">
    <!-- <q-img
      fit="scale-down"
      v-show="show"
      src="./images/21497_Lockdown.png"
      style="height: 500px; max-width: 750px;"
    /> -->
  
  <img v-show="show1" src="./images/AS55836_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show2" src="./images/AS55836IN_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show3" src="./images/AS55836IN_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show4" src="./images/AS2516_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show5" src="./images/AS2516_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show6" src="./images/AS2516_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show7" src="./images/AS17676_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show8" src="./images/AS17676_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show9" src="./images/AS17676_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show10" src="./images/AS4713JP_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show11" src="./images/AS4713JP_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show12" src="./images/AS4713JP_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show13" src="./images/AS15895UA_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show14" src="./images/AS15895UA_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show15" src="./images/AS15895UA_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show16" src="./images/AS21497_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show17" src="./images/AS21497_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show18" src="./images/AS21497_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show19" src="./images/AS6849UA_Lockdown.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show20" src="./images/AS6849UA_Latest.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  <img v-show="show21" src="./images/AS6849UA_onemonth.png" style="padding-left: 25%; height: 500px; max-width: 750px;">
  </div>
</template>


<script>
import { defineComponent } from 'vue'
import { ref } from 'vue'

export default defineComponent({
  name: 'App',
  data(){
    return{
      show1:false,
      show2:false,
      show3:false,
      show4:false,
      show5:false,
      show6:false,
      show7:false,
      show8:false,
      show9:false,
      show10:false,
      show11:false,
      show12:false,
      show13:false,
      show14:false,
      show15:false,
      show16:false,
      show17:false,
      show18:false,
      show19:false,
      show20:false,
      show21:false
    }
  },
  setup () {
    return {
      models: ref(null),
      sourceoptions: [
         'IN AS55836 Reliance Jio Limited','JP AS2516 KDDI KDDI CORPORATION','JP AS17676 GIGAINFRA Softbank BB Corp','JP AS4713 OCN NTT Communications','UA AS15895 KSNET "Kyivstar"','UA AS21497 UMC-AS','UA AS6849 UKRTELNET "Ukrtelecom"'
      ],
      modeld: ref(null),
      destinationoptions: [
        'India','Japan', 'Ukraine'
      ],
      modelt: ref(null),
      timeperiodoptions: [
        'one_month_before_lockdown', 'LockDown', 'Latest'
      ],
      modelm: ref(null),
      metricsoptions: [
        'Median RTT (ms)'
      ]
    }
  },
  methods:{
    submit() {
        if((this.models=='IN AS55836 Reliance Jio Limited') && (this.modelt=='Latest')){
          this.show1=true
        }
        if((this.models=='IN AS55836 Reliance Jio Limited') && (this.modelt=='one_month_before_lockdown')){
          this.show2=true
        }
        if((this.models=='IN AS55836 Reliance Jio Limited') && (this.modelt=='LockDown')){
          this.show3=true
        }
        // japan
        if((this.models=='JP AS2516 KDDI KDDI CORPORATION') && (this.modelt=='LockDown')){
          this.show4=true
        }
        if((this.models=='JP AS2516 KDDI KDDI CORPORATION') && (this.modelt=='Latest')){
          this.show5=true
        }
        if((this.models=='JP AS2516 KDDI KDDI CORPORATION') && (this.modelt=='one_month_before_lockdown')){
          this.show6=true
        }
        if((this.models=='JP AS17676 GIGAINFRA Softbank BB Corp') && (this.modelt=='one_month_before_lockdown')){
          this.show7=true
        }
        if((this.models=='JP AS17676 GIGAINFRA Softbank BB Corp') && (this.modelt=='Latest')){
          this.show8=true
        }
        if((this.models=='JP AS17676 GIGAINFRA Softbank BB Corp') && (this.modelt=='LockDown')){
          this.show9=true
        }
        if((this.models=='JP AS4713 OCN NTT Communications') && (this.modelt=='LockDown')){
          this.show10=true
        }
        if((this.models=='JP AS4713 OCN NTT Communications') && (this.modelt=='one_month_before_lockdown')){
          this.show11=true
        }
        if((this.models=='JP AS4713 OCN NTT Communications') && (this.modelt=='Latest')){
          this.show12=true
        }
        //ukraine
        if((this.models=='UA AS15895 KSNET "Kyivstar"') && (this.modelt=='LockDown')){
          this.show13=true
        }
        if((this.models=='UA AS15895 KSNET "Kyivstar"') && (this.modelt=='Latest')){
          this.show14=true
        }
        if((this.models=='UA AS15895 KSNET "Kyivstar"') && (this.modelt=='one_month_before_lockdown')){
          this.show15=true
        }
        if((this.models=='UA AS21497 UMC-AS') && (this.modelt=='one_month_before_lockdown')){
          this.show16=true
        }
        if((this.models=='UA AS21497 UMC-AS') && (this.modelt=='Latest')){
          this.show17=true
        }
        if((this.models=='UA AS21497 UMC-AS') && (this.modelt=='LockDown')){
          this.show18=true
        }
        if((this.models=='UA AS6849 UKRTELNET "Ukrtelecom"') && (this.modelt=='LockDown')){
          this.show19=true
        }
        if((this.models=='UA AS6849 UKRTELNET "Ukrtelecom"') && (this.modelt=='Latest')){
          this.show20=true
        }
        if((this.models=='UA AS6849 UKRTELNET "Ukrtelecom"') && (this.modelt=='one_month_before_lockdown')){
          this.show21=true
        }

      }
  }
})

</script>

<style>

.inputs{
  align-items: center;
  padding-left: 40%;
  justify-content: center;
}
h2{
  text-align: center;
  justify-content: center;
}

.btns{
  padding-top: 40px;
}
.userbox{
  padding-top: 20px;
}
.hintbtn{
  border-radius: 10px;
}
p{
  padding:0% 20% 0% 20%;
  font-size: 1.5rem;
  text-align: justify;
}

</style>
