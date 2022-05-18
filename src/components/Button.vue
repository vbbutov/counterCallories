<template>
<section>
     <div class="form__submit">
       <div v-if="unlockCounter">
             <button @click="computeCal" class="form__submit-button button" name="submit" type="submit">
              Рассчитать
            </button>
       </div>
       <div v-else >
             <button class="form__submit-button button" name="submit" type="submit" disabled>
              Рассчитать
            </button>
       </div>
       <div>
            <button v-if="unlockReset" @click="resetChild" class="form__reset-button" name="reset" type="reset" >
              <svg width="24" height="24" viewbox="0 0 24 24" fill="#FD3636" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M13.4143 12.0002L18.7072 6.70725C19.0982 6.31625 19.0982 5.68425 18.7072 5.29325C18.3162 4.90225 17.6842 4.90225 17.2933 5.29325L12.0002 10.5862L6.70725 5.29325C6.31625 4.90225 5.68425 4.90225 5.29325 5.29325C4.90225 5.68425 4.90225 6.31625 5.29325 6.70725L10.5862 12.0002L5.29325 17.2933C4.90225 17.6842 4.90225 18.3162 5.29325 18.7072C5.48825 18.9022 5.74425 19.0002 6.00025 19.0002C6.25625 19.0002 6.51225 18.9022 6.70725 18.7072L12.0002 13.4143L17.2933 18.7072C17.4882 18.9022 17.7443 19.0002 18.0002 19.0002C18.2562 19.0002 18.5122 18.9022 18.7072 18.7072C19.0982 18.3162 19.0982 17.6842 18.7072 17.2933L13.4143 12.0002Z"/>
              </svg>
              <span>
                Очистить поля и расчёт
              </span>
            </button>
            <button v-else class="form__reset-button" name="reset" type="reset" disabled>
              <svg width="24" height="24" viewbox="0 0 24 24" fill="#FD3636" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" clip-rule="evenodd" d="M13.4143 12.0002L18.7072 6.70725C19.0982 6.31625 19.0982 5.68425 18.7072 5.29325C18.3162 4.90225 17.6842 4.90225 17.2933 5.29325L12.0002 10.5862L6.70725 5.29325C6.31625 4.90225 5.68425 4.90225 5.29325 5.29325C4.90225 5.68425 4.90225 6.31625 5.29325 6.70725L10.5862 12.0002L5.29325 17.2933C4.90225 17.6842 4.90225 18.3162 5.29325 18.7072C5.48825 18.9022 5.74425 19.0002 6.00025 19.0002C6.25625 19.0002 6.51225 18.9022 6.70725 18.7072L12.0002 13.4143L17.2933 18.7072C17.4882 18.9022 17.7443 19.0002 18.0002 19.0002C18.2562 19.0002 18.5122 18.9022 18.7072 18.7072C19.0982 18.3162 19.0982 17.6842 18.7072 17.2933L13.4143 12.0002Z"/>
              </svg>
              <span>
                Очистить поля и расчёт
              </span>
            </button>
        </div>
          </div>
           <my-result :result="computeCallories"></my-result>
</section>
</template>
<script lang="ts">
/* eslint-disable eqeqeq */
import { defineComponent } from 'vue'
import MyResult from '@/components/Result.vue'
// import {constants} from '@/constants'
export default defineComponent({
  name: 'button-page',
  props: ['height', 'weight', 'age', 'physicalActivity', 'gender'],
  components: {MyResult},
  methods: {
    resetChild () :void {
      this.$emit('updateParent')
    },
    computeCal () {
      this.$emit('compute')
    }
  },
  computed: {
    unlockReset ():boolean {
      // console.log(this.height === '' || this.weight === '' ||
      //   this.age === '' || this.physicalActivity === '')
      if (this.height !== 0 || this.weight !== 0 ||
        this.age !== 0) {
        return true
      }
      return false
    },
    unlockCounter ():boolean {
      // console.log('uuuuuu' + this.height === '' && this.weight === '' &&
      //  this.age === '')
      if (this.height !== 0 && this.weight !== 0 &&
        this.age !== 0) {
        return true
      }
      return false
    }

  }

})
</script>
