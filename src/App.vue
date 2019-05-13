<template>
  <div id="app">
    <div class="main col-md-6 form-group">
      <h2>Настройки</h2>

      <div class="form-group">
        <span>Дата старта</span>
        <Datepicker/>
      </div>

      <div class="form-group">
          <div class="form-check">
            <input
              class="form-check-input"
              type="checkbox"
              name="withEndDate"
              id="with-end-date"
              v-model="withDateEnd">
            <label class="form-check-label" for="with-end-date">Дата окончания</label>
          </div>

          <transition name="fade">
            <Datepicker v-if="withDateEnd"/>
          </transition>
      </div>
    </div>

    <!-- Правило -->
    <div class="rule col-md-6 form-group">
      <!-- <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          name="withEvent"
          id="with-event"
          v-model="withEvent">
        <label class="form-check-label" for="with-event">Событие</label>
      </div> -->

      <div :class="{ 'disabled': !withEvent }">
        <div class="form-group">
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="inlineRadioOptions"
              id="oneTimeSale"
              value="oneTimeSale"
              v-model="ruleType">
            <label class="form-check-label" for="oneTimeSale" selected>Единоразовая акция</label>
          </div>

          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadio1"
              value="sale"
              v-model="ruleType">
            <label class="form-check-label" for="inlineRadio1">Покупка</label>
          </div>

          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadio2"
              value="outflow"
              v-model="ruleType">
            <label class="form-check-label" for="inlineRadio2">Отток</label>
          </div>

          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="inlineRadioOptions"
              id="inlineRadio3"
              value="birthday"
              v-model="ruleType">
            <label class="form-check-label" for="inlineRadio3">День рождения</label>
          </div>
        </div>

        <transition name="fade">
          <div class="rule__settings rule-settings">
            <div class="rule-settings__sale" v-if="ruleType === 'outflow'">
              <div class="form-group">
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="outlineSettings"
                    id="inlineRadio2"
                    value="outflow"
                    v-model="ruleType">
                  <label class="form-check-label" for="inlineRadio2">Не было N-дней</label>
                </div>

                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="outlineSettings"
                    id="inlineRadio3"
                    value="birthday"
                    v-model="ruleType">
                  <label class="form-check-label" for="inlineRadio3">Дата последней покупки</label>
                </div>
              </div>
            </div>

            <div class="rule-settings__date" v-if="ruleType === 'date'">
              <Datepicker/>
            </div>

            <div class="rule-settings__sale" v-if="ruleType === 'sale'">
              <!-- Начисление при покупке от -->
              <div class="form-group">
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    name="inlineRadioOptions"
                    id="first-sale">
                  <label class="form-check-label" for="first-sale">Первая покупка</label>
                </div>

                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    name="inlineRadioOptions"
                    id="with-points-from"
                    v-model="withPointsFrom"
                  >
                  <label class="form-check-label" for="with-points-from">При покупке от</label>
                </div>

                <input
                  type="email"
                  class="form-control"
                  id="points-amount"
                  aria-describedby="emailHelp"
                  placeholder="Сумма покупки"
                  :disabled="!withPointsFrom">
              </div>
            </div>
          </div>
        </transition>
      </div>
    </div>

    <!-- Баллы -->
    <div class="points col-md-6 form-group">
      <h2>Действия</h2>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          name="inlineRadioOptions"
          id="with-points"
          v-model="withPoints"
        >
        <label class="form-check-label" for="with-points">Начисление баллов</label>
      </div>

      <transition name="fade">
        <div class="points__settings" v-if="withPoints">
          <div class="form-group">
            <label for="points-amount">Бонусные баллы</label>
            <input
              type="email"
              class="form-control"
              id="points-amount"
              aria-describedby="emailHelp"
              placeholder="Бонусные баллы"
            >
          </div>

          <!-- Дата старта трат -->
          <div class="points-start-spend form-group">
            <label for="exampleInputEmail1">Дата начала использования</label>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                name="startType"
                id="startType1"
                value="option2"
              >
              <label class="form-check-label" for="startType1">С момента начисления</label>
            </div>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                name="startType"
                id="startType2"
                value="option3"
              >
              <label class="form-check-label" for="startType2">Спустя фиксированное время</label>
            </div>
            <div class="form-check">
              <input
                class="form-check-input"
                type="radio"
                name="startType"
                id="startType3"
                value="option4"
              >
              <label class="form-check-label" for="startType3">Дата</label>
            </div>
          </div>

          <!-- Сгорают -->
          <div class="points-can-burn form-group">
            <div class="form-check">
              <input
                class="form-check-input"
                type="checkbox"
                name="inlineRadioOptions"
                id="points-can-burn"
                v-model="pointsCanBurn"
              >
              <label for="points-can-burn">Сгорают</label>
            </div>

            <transition name="fade">
              <div class="points-can-burn__settings" v-if="pointsCanBurn">
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="burnType"
                    id="burnType1"
                    value="option1"
                  >
                  <label class="form-check-label" for="burnType1">С окончанием кампании</label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="burnType"
                    id="burnType2"
                    value="option2"
                  >
                  <label class="form-check-label" for="burnType2">Фиксированная длительность</label>
                </div>
                <div class="form-check">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="burnType"
                    id="burnType3"
                    value="option3"
                  >
                  <label class="form-check-label" for="burnType3">Дата</label>
                </div>
              </div>
            </transition>
          </div>
        </div>
      </transition>

      <div class="notification">
          <div class="form-group">
            <div class="form-check">
              <input
                class="form-check-input"
                type="checkbox"
                name="withNotify"
                id="withNotify"
                v-model="withNotify">
              <label class="form-check-label" for="withNotify">Уведомление по СМС</label>
            </div>
          </div>

          <transition name="fade">
            <div class="form-group" v-if="withNotify">
              <label for="#">Текст СМС</label>
              <textarea class="form-control" rows="3"></textarea>
            </div>
          </transition>
        </div>
    </div>

    <!-- Аудитория -->
    <div class="audience col-md-4 form-group">
      <h2>Аудитория</h2>

      <div class="points-start-spend form-group">
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="audienceType"
            id="audienceType1"
            value="all"
            v-model="selectedAudienceType"
          >
          <label class="form-check-label" for="audienceType1">Все</label>
        </div>
        <div class="form-check">
          <input
            class="form-check-input"
            type="radio"
            name="audienceType"
            id="audienceType2"
            value="dynamic"
            v-model="selectedAudienceType"
          >
          <label class="form-check-label" for="audienceType2">Динамическая</label>
        </div>
        <div class="form-group">
          <div class="form-check">
            <input
              class="form-check-input"
              type="radio"
              name="audienceType"
              id="audienceType3"
              value="static"
              v-model="selectedAudienceType"
            >
            <label class="form-check-label" for="audienceType3">Статическая</label>
          </div>
        </div>

        <transition name="fade">
          <div class="audience__static-filter"
            v-if="selectedAudienceType === 'static'">
            <textarea
              class="form-control"
              rows="3">
            </textarea>
          </div>

          <div class="audience__dynamic-filter"
            v-if="selectedAudienceType === 'dynamic'">
            <div class="form-group">
              <span>Возраст</span>
              <div class="form-row">
                <div class="col-md-6">
                  <input type="text" class="form-control" id="validationCustom01" placeholder="От" required>
                </div>
                <div class="col-md-6">
                  <input type="text" class="form-control" id="validationCustom02" placeholder="До" required>
                </div>
              </div>
            </div>

            <div class="form-group">
              <span>Пол</span>
              <div class="form-check">
                <input
                  class="form-check-input"
                  type="radio"
                  name="audienceType"
                  id="gender1"
                  value="dynamic"
                  v-model="selectedAudienceType">
                <label class="form-check-label" for="gender1">Мужской</label>
              </div>
              <div class="form-check">
                <input
                  class="form-check-input"
                  type="radio"
                  name="audienceType"
                  id="gender2"
                  value="dynamic"
                  v-model="selectedAudienceType">
                <label class="form-check-label" for="gender2">Женский</label>
              </div>
            </div>
          </div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker';


export default {
  name: 'app',

  components: {
    Datepicker,
  },

  data() {
    return {
      withDateEnd: false,
      withEvent: true,
      withPoints: true,
      withPointsFrom: false,
      withNotify: false,
      pointsCanBurn: false,

      selectedAudienceType: 'all',
      ruleType: '',
    };
  },
};
</script>

<style lang="scss" src="./styles/index.scss"></style>
<style lang="scss">
#app {
  font-family: "Comfortaa", cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.disabled {
  pointer-events: none;
  opacity: 0.3;
}
</style>
