<template>
<div>
            <form class="counter__form form" name="counter" action="#" method="post">
          <div class="form__item">
            <h2 class="heading">
              Пол
            </h2>
            <ul class="switcher">
              <li class="switcher__item">
                <input v-model="gender" id="gender-male" name="gender" value="male" type="radio"  required>
                <label for="gender-male">
                  Мужчина
                </label>
              </li>
              <li class="switcher__item">
                <input v-model="gender"  id="gender-female" name="gender" value="female" type="radio" required>
                <label for="gender-female">
                  Женщина
                </label>
              </li>
            </ul>
          </div>
          <fieldset class="form__item form__parameters" name="parameters">
            <legend class="visually-hidden">
              Физические параметры
            </legend>
            <div class="inputs-group">
              <div class="input">
                <div class="input__heading">
                  <label class="heading" for="age">
                    Возраст
                  </label>
                  <span class="input__heading-unit">
                    лет
                  </span>
                </div>
                <div class="input__wrapper">
                  <input v-model="age"  type="text" id="age" name="age" placeholder="0" inputmode="decimal" maxlength="3" required>
                </div>
              </div>
              <div class="input">
                <div class="input__heading">
                  <label class="heading" for="height">
                    Рост
                  </label>
                  <span class="input__heading-unit">
                    см
                  </span>
                </div>
                <div class="input__wrapper">
                  <input v-model="height" type="text" id="height" name="height" placeholder="0" inputmode="decimal" maxlength="3" required>
                </div>
              </div>
              <div class="input">
                <div class="input__heading">
                  <label class="heading" for="weight">
                    Вес
                  </label>
                  <span class="input__heading-unit">
                    кг
                  </span>
                </div>
                <div class="input__wrapper">
                  <input v-model="weight" type="number" id="weight" name="weight" placeholder="0" inputmode="decimal" maxlength="3" required>
                </div>
              </div>
            </div>
          </fieldset>
          <fieldset class="form__item">
                    <legend class="heading">
                      Физическая активность
                    </legend>
                    <ul class="radios-group">
                      <li class="radio">
                        <div class="radio__wrapper">
                          <input v-model="physicalActivity" value="min"  id="activity-minimal" name="activity" type="radio" checked required>
                          <label for="activity-minimal">
                            Минимальная
                          </label>
                        </div>
                        <p class="radio__description">
                          Сидячая работа и нет физических нагрузок
                        </p>
                      </li>
                      <li class="radio">
                        <div class="radio__wrapper">
                          <input v-model="physicalActivity" value="low"  id="activity-low" name="activity"  type="radio" required>
                          <label for="activity-low">
                            Низкая
                          </label>
                        </div>
                        <p class="radio__description">
                          Редкие, нерегулярные тренировки, активность в быту
                        </p>
                      </li>
                      <li class="radio">
                        <div class="radio__wrapper">
                          <input v-model="physicalActivity" id="activity-medium" name="activity" value="medium" type="radio" required>
                          <label for="activity-medium">
                            Средняя
                          </label>
                        </div>
                        <p class="radio__description">
                          Тренировки 3-5 раз в неделю
                        </p>
                      </li>
                      <li class="radio">
                        <div class="radio__wrapper">
                          <input v-model.lazy="physicalActivity" id="activity-high" name="activity" value="high" type="radio" required>
                          <label for="activity-high">
                            Высокая
                          </label>
                        </div>
                        <p class="radio__description">
                          Тренировки 6-7 раз в неделю
                        </p>
                      </li>
                      <li class="radio">
                        <div class="radio__wrapper">
                          <input v-model="physicalActivity" id="activity-maximal" name="activity" value="max" type="radio" required>
                          <label for="activity-maximal">
                            Очень высокая
                          </label>
                        </div>
                        <p class="radio__description">
                          Больше 6 тренировок в неделю и физическая работа
                        </p>
                      </li>
                    </ul>
          </fieldset>
          <my-result></my-result>
        </form>
          <my-button :age="age" :height="height" :physicalActivity="physicalActivity" :weight="weight" :gender="gender" @updateParent='resetData'
          @compute="computeCallories"></my-button>
          <div v-if="result >= 0">
               <my-result :result="result"></my-result>
          </div>
          <div v-else>
             Введены некорректные данные : {{result.toFixed(2)}}
          </div>

        </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import MyButton from '@/components/Button.vue'
import MyResult from '@/components/Result.vue'
export default defineComponent({
  name: 'main-form',
  components: { MyButton, MyResult },

  data () {
    return {
      height: 0,
      weight: 0,
      age: 0,
      gender: 'male',
      physicalActivity: 'min',
      coefficient: 0,
      result: 0
    }
  },
  methods: {
    resetData () {
      this.height = 0
      this.weight = 0
      this.age = 0
      this.physicalActivity = 'min'
      this.gender = 'male'
      this.result = 0
    },
    computeCallories ():number {
      this.result = (10 * this.weight) + (6.26 * this.height) - (5 * this.age)
      if (this.gender === 'male') {
        this.result -= 161
      } else {
        console.log(this.result)
        this.result += 5
      }
      let x = 0
      switch (this.physicalActivity) {
        case 'min': x = 1.2; break
        case 'low': x = 1.375; break
        case 'medium':x = 1.55; break
        case 'high' : x = 1.725; break
        case 'max': x = 1.9; break
      }
      console.log(x)
      console.log(this.result * x)
      this.result *= x
      return this.result
    }
  }
})
</script>
