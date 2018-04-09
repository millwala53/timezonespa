<template>
    <div class="slider">
        <span class="slider__marker">
        </span>
        <div ref="tape" class="slider__tape">
            <div class="hour">
              <span class="time">12 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">1 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">2 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">3 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">4 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">5 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">6 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">7 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">8 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">9 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">10 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">11 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">12 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">1 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">2 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">3 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">4 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">5 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">6 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">7 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">8 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">9 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">10 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">11 PM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
            <div class="hour">
              <span class="time">12 AM</span>
              <span class="hour_mark"></span>
              <span class="quarter_mark"></span>
              <span class="half_mark"></span>
              <span class="second_quarter_mark"></span>
            </div>
        </div>
    </div>
</template>

<script>
import Hammer from 'hammerjs'

export default {
  props: ['time'],
  data () {
    return {
      currentTranslate: 0,
      mid: 0
    }
  },
  watch: {
    time () {
      this.currentTranslate = (this.time * -0.02849537037) + this.mid
      this.$refs.tape.style.transform = 'translateX(' + this.currentTranslate + 'px)'
    }
  },
  mounted () {
    this.windowWidth = window.innerWidth
    this.mid = this.windowWidth / 2

    // this.$refs.tape.style.transform = 'translateX(' + this.mid + 'px)'

    this.currentTranslate = (this.time * -0.02849537037) + this.mid
    this.$refs.tape.style.transform = 'translateX(' + this.currentTranslate + 'px)'

    var hammertime = new Hammer(this.$refs.tape)

    hammertime.on('panright', () => {
      this.$emit('panright')
    })

    hammertime.on('panleft', () => {
      this.$emit('panleft')
    })

    window.addEventListener('resize', () => {
      this.windowWidth = window.innerWidth
      this.mid = this.windowWidth / 2

      this.currentTranslate = (this.time * -0.02849537037) + this.mid
      this.$refs.tape.style.transform = 'translateX(' + this.currentTranslate + 'px)'
    })
  }
}
</script>

<style lang="scss" scoped>
    .slider {
        height: 100px;
        position: relative;
        display: inline-flex;

        // padding-top: 10px;

        &__tape {
            // transition: transform .2s ease;
            height: 100%;
            // padding: 0 20px;
            // overflow-x: scroll;
            white-space: nowrap;

            .hour {
              display: inline-block;
              color: white;
              height: calc(100% - 10px);

              position: relative;

              .time {
                font-size: 16px;
                position: absolute;
                transform: translateX(-50%);
              }

              .hour_mark {
                position: absolute;
                left: 0;
                bottom: 0;
                height: 40px;
                width: 2px;
                background-color: white;
                display: block;
              }

              .quarter_mark {
                position: absolute;
                left: 25%;
                bottom: 0;
                height: 15px;
                width: 2px;
                background-color: white;
                display: block;
              }

              .second_quarter_mark {
                position: absolute;
                left: 75%;
                bottom: 0;
                height: 15px;
                width: 2px;
                background-color: white;
                display: block;
              }

              .half_mark {
                position: absolute;
                left: 50%;
                bottom: 0;
                height: 25px;
                width: 2px;
                background-color: white;
                display: block;
              }

              &:not(:last-child) {
                width: 100px;
              }
            }
        }

        &__marker {
            position: absolute;
            bottom: 0;
            left: 50%;

            transform: translateX(-50%);

            &::before {
                content: '';
                display: block;
                color: white;

                width: 0px;
                height: 0px;

                border-left: 10px solid transparent;
                border-right: 10px solid transparent;

                border-bottom: 10px solid white;
            }
        }
    }
</style>
