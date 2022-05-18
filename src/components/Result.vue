<template>
        <section v-show="status" class="counter__result counter__result--hidden">
            <h2 class="heading">Ваша норма калорий</h2>
            <ul class="counter__result-list">
                <li class="counter__result-item">
                    <h3><span id="calories-norm">{{outResultForSupportWeiht}}</span> ккал</h3>
                    <p>поддержание веса</p>
                </li>
                <li class="counter__result-item">
                    <h3><span id="calories-minimal">{{outResultForFallWeight}}</span> ккал</h3>
                    <p>снижение веса</p>
                </li>
                <li class="counter__result-item">
                    <h3><span id="calories-maximal">{{outResultForUpWeight}}</span> ккал</h3>
                    <p>набор веса</p>
                </li>
            </ul>
        </section>
</template>
<script lang="ts">
import { Vue } from 'vue-class-component'
import { Prop } from 'vue-property-decorator'
export default class MyResult extends Vue {
    @Prop() result!:number;

    get outResultForSupportWeiht ():string {
      if (this.status === false) {
        return ''
      }
      return this.result.toFixed(2)
    }

    get outResultForFallWeight ():string {
      const r = this.result - ((this.result / 100) * 20)
      return r.toFixed(2)
    }

    get outResultForUpWeight () {
      const r = this.result + ((this.result / 100) * 20)
      return r.toFixed(2)
    }

    get status ():boolean {
      if (this.result > 0) {
        return true
      }
      return false
    }
}
</script>
