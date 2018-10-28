<template>
  <div class="home">
    <div class="dialog">
      <div class="dialog-header">
        <div class="tab" :class="(step === 1) ? 'active': ''">
          Describe your dream
        </div>
        <div class="tab" :class="(step === 2) ? 'active': ''">
          Enter dream info
        </div>
        <div class="tab" :class="(step === 3) ? 'active': ''">
          
          Share?
        </div>
      </div>
      <div class="dialog-content" v-if='step === 1'>

        <b-form-textarea
          v-model="description"
          placeholder="Describe your dream in details"
          :rows="4"
          :max-rows="8">
        </b-form-textarea>

      
      </div>
      <div class="dialog-content" v-if='step === 2'>
        <label>
          When you want it?

          <b-form-select v-model="when" :options="whenOptions" />
        </label>
        <label>
          How strong your wish?
          <b-form-input :type="'number'" v-model="dreamPower"
            placeholder='Enter value from 1 to 10' min="1" max="10"
          ></b-form-input>

        </label>
      </div>
      <div class="dialog-content" v-if='step === 3'>
         <b-form-group label="Want to share with others?">
          <b-form-radio-group v-model="share"
                        :options="shareOptions"
                        stacked>
          </b-form-radio-group>
        </b-form-group>
      </div>
      <div class="button-holder">

        <b-button @click="step -= 1" v-if="step > 1" >
            <font-awesome-icon icon="arrow-left" />
            Prev
        </b-button>
        <div></div>
        <b-button @click="step += 1" v-if="step < 3">
            Next <font-awesome-icon icon="arrow-right" />
        </b-button>
        <b-button @click="saveDream" v-else>
            <font-awesome-icon icon="check-double" />
            Complete
        </b-button>

      </div>
    </div>
  </div>
</template>

<script>
import '../icons';
import { mapActions } from 'vuex';

export default {
  name: 'home',
  data() {
    return {
      step: 1,
      description: '',
      when: 'afteraweek',
      dreamPower: 5,
      whenOptions: [
        { value: 'afteraweek', text: 'After a week' },
        { value: 'afteramonth', text: 'After a month' },
        { value: 'afterayear', text: 'After a year' },
      ],
      share: 'no',
      shareOptions: [
        { value: 'yes', text: 'Yes' },
        { value: 'no', text: 'No' },
      ]
    }
  },
  methods: {
    ...mapActions(['actionSaveDream']),
    saveDream() {
      const dream = {
        description: this.description,
        when: this.when,
        dreamPower: this.dreamPower,
        share: this.share
      };
      this.actionSaveDream(dream);
      this.$router.push({name:'list'})
    }

  }
}
</script>

<style>
.custom-control-label::before {
  background-color: #a2c0df;
}

</style>

<style lang="scss" scoped>


$dlg-color: rgb(228, 228, 228);
$border-radius: 15px;
.home {
  background: rgba(white, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top:0;
  bottom: 0;
  right: 0;
  left: 0;

  .dialog {
    background-color: $dlg-color;
    width: 700px;
    height: 350px;
    border-radius: $border-radius;
    box-shadow: 0 0 20px darken($dlg-color, 30);
    display: flex;
    flex-direction: column;

    .dialog-header {
      display: flex;
      justify-content: space-between;
      height: 60px;
      .tab {
        &:not(.active) {
          background-color: darken($dlg-color, 30);
          color: white;

          &:last-of-type {
            border-top-right-radius: $border-radius;
          }

          &:first-of-type {
            border-top-left-radius: $border-radius;
          }
        }

        &.active {
          font-weight: bold;
        }
        width: 100%;
        
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }

    .dialog-content {
      padding: 30px;
      flex-grow: 1;
      display: flex;
      flex-direction: column;
    }
    .button-holder {
      display: flex;
      justify-content: space-between;
      padding: 30px;
    }
  }
}


</style>
