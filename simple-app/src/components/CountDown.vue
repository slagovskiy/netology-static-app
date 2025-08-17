<template>
  <div class="countdown">
    <h1>До Нового Года осталось:</h1>
    <div class="timer">
      {{ days }} дней : {{ hours }} часов : {{ minutes }} минут : {{ seconds }} секунд
    </div>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'CountDown',
  data() {
    return {
      intervalId: null,
      newYearDate: moment('2026-01-01'), // Дата наступления следующего Нового Года
      now: moment(),
    };
  },
  computed: {
    diffInMilliseconds() {
      return this.newYearDate.diff(this.now); // разница в миллисекундах
    },
    days() {
      return Math.floor(moment.duration(this.diffInMilliseconds).asDays());
    },
    hours() {
      const remainingHours = moment.duration(this.diffInMilliseconds).hours();
      return ('0' + remainingHours).slice(-2); // форматируем часы с ведущими нулями
    },
    minutes() {
      const remainingMinutes = moment.duration(this.diffInMilliseconds).minutes();
      return ('0' + remainingMinutes).slice(-2); // форматируем минуты с ведущими нулями
    },
    seconds() {
      const remainingSeconds = moment.duration(this.diffInMilliseconds).seconds();
      return ('0' + remainingSeconds).slice(-2); // форматируем секунды с ведущими нулями
    },
  },
  mounted() {
    this.intervalId = setInterval(() => {
      this.now = moment(); // обновляем текущее время каждые секунду
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.intervalId); // отключаем таймер при уничтожении компонента
  },
};
</script>

<style scoped>
.countdown {
  text-align: center;
  font-family: Arial, sans-serif;
}
.timer {
  font-size: 2rem;
  color: #ff4500;
}
</style>