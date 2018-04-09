<template>
  <div class="background">
    <div @click="showAdd = !showAdd" :class="{'active': showAdd}" class="nav-btn">
      <span>&nbsp;</span>
      <span>&nbsp;</span>
      <span>&nbsp;</span>
    </div>

    <transition name="zoom">
      <span @click="reset" v-if="panned" class="reset">
        <i class="fa fa-refresh"></i>
      </span>
    </transition>

    <ul class="list">
      <li :class="{selected: location.selected}" @click="select(location, i)" v-for="(location, i) in locations" class="list__item">
        <div>
          <span class="list__item__name"> {{ location.name }} </span>
          <span class="list__item__timeoffset"> {{ getOffset(location, i) }} <span> {{ getCurrentTime(location) | moment("ddd") }} </span> </span>
        </div>
        <div>
          <span class="list__item__time">
            {{ getCurrentTime(location) | moment("hh:mm") }}
            <span> {{ getCurrentTime(location) | moment("A") }} </span>
          </span>
        </div>
      </li>
    </ul>
    <app-slider @panright="sliderPanRight" @panleft="sliderPanLeft" :time="offsetSinceMidnight"></app-slider>
    <transition name="slide">
      <app-add @cityAdded="cityAdded" @close="showAdd = false" v-if="showAdd"></app-add>
    </transition>
  </div>
</template>

<script>
import Add from './Add'
import Slider from './Slider'

export default {
  components: {
    'app-add': Add,
    'app-slider': Slider
  },
  data () {
    return {
      localTime: new Date().getTime(),
      localOffset: new Date().getTimezoneOffset(),
      utcTime: '',
      panned: false,
      showAdd: false,
      currentIndex: 0,
      locations: [
        {
          name: 'My Location',
          utc_offset: Math.abs(new Date().getTimezoneOffset()),
          selected: true
        }
      ]
    }
  },
  computed: {
    offsetSinceMidnight () {
      var now = new Date(this.utcTime + this.locations[this.currentIndex].utc_offset * 60000)
      var lastMidnight = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 0, 0, 0)

      return (now.getTime() - lastMidnight.getTime()) / 1000
    }
  },
  methods: {
    reset () {
      this.utcTime = this.localTime + (this.localOffset * 60000)
      this.panned = false
    },
    sliderPanRight () {
      this.panned = true
      this.utcTime -= 180000
    },
    sliderPanLeft () {
      this.panned = true
      this.utcTime += 180000
    },
    cityAdded (cityData) {
      cityData.selected = false
      this.locations.push(cityData)

      this.updateLocalStorage()
    },
    getCurrentTime (location) {
      return new Date(this.utcTime + location.utc_offset * 60000)
    },
    getOffset (location, index) {
      if (index === this.currentIndex) {
        return '+00:00'
      } else {
        var currentSelection = this.locations[this.currentIndex]
        var currentOffset = currentSelection.utc_offset
        var locationOffset = location.utc_offset

        if (locationOffset >= currentOffset) {
          return this.toOffsetString('+', locationOffset - currentOffset)
        } else {
          return this.toOffsetString('-', currentOffset - locationOffset)
        }
      }
    },
    toOffsetString (sign, number) {
      var remainder = '' + number % 60
      var string = '' + number / 60

      if (remainder.length === 1) {
        remainder = '0' + remainder
      }

      if (string.length === 1) {
        string = '0' + string
      }

      return sign + string + ':' + remainder
    },
    select (location, index) {
      this.locations[this.currentIndex].selected = false
      location.selected = true
      this.currentIndex = index
    },
    updateLocalStorage () {
      var temp = this.locations.slice()
      temp = temp.splice(1, temp.length - 1)

      temp.forEach(location => {
        location.selected = false
      })

      localStorage.setItem('locations', JSON.stringify(temp))
    }
  },
  created () {
    var savedLocations = JSON.parse(localStorage.getItem('locations'))

    if (savedLocations) {
      savedLocations.forEach(location => {
        this.locations.push(location)
      })
    }

    this.utcTime = this.localTime + (this.localOffset * 60000)

    setInterval(() => { // Start off an interval that ticks each second to update time every second
      this.utcTime += 1000
    }, 1000)
  }
}
</script>

<style lang="scss" scoped>
  .background {
    height: 100vh;
    width: 100%;

    overflow-x: hidden;

    display: flex;
    flex-direction: column;
    justify-content: start;

    background-color: #27203F;
  }

  .reset {
    display: flex;

    justify-content: center;
    align-items: center;

    position: absolute;
    top: 10px;
    right: 10px;

    width: 35px;
    height: 35px;

    background-color: white;

    border-radius: 50%;

    i {
      font-size: 20px;
    }
  }

  .nav-btn {
    width: 35px;
    height: 35px;

    z-index: 10;

    position: absolute;
    top: 10px;
    left: 10px;

    background-color: white;

    border-radius: 50%;

    display: flex;
    flex-direction: column;

    justify-content: center;
    align-items: center;

    span {
      display: block;
      position: relative;
      height: 2px;
      width: 20px;
      background-color: black;
      top: 0;

      &:not(:last-child) {
        margin-bottom: 2px;
      }

      transition: all .3s ease-in;
    }
  }

  .nav-btn.active {
    span:nth-child(2) {
      width: 0;
      opacity: 0;
    }

    span:nth-child(1) {
      transform: rotate(45deg);
      top: 4px;
    }

    span:nth-child(3) {
      transform: rotate(-45deg);
      top: -4px;
    }
  }

  .list {
    margin-top: 60px;
    padding: 0 2rem 2rem;

    list-style: none;
    flex: 1 0;

    overflow-y: auto;

    &__item {
      padding: 20px 0;
      color: white;

      font-size: 2rem;

      border-bottom: 1.5px solid rgba(207, 207, 207, 0.25);

      display: flex;
      justify-content: space-between;
      align-items: center;

      &__name {
        margin-bottom: 10px;
        font-size: 2rem;

        text-shadow: 2px 2px 3px rgba(0, 0, 0, .5);

        display: block;
      }

      &__timeoffset {
        color: #e2e2e2;
        font-size: 1.5rem;

        text-shadow: 2px 2px 3px rgba(0, 0, 0, .5);

        span {
          padding: 2px 5px;
          background-color: rgba(0, 0, 0, .25);
          font-size: 12px;
          text-transform: uppercase;
        }
      }

      &__time {
        font-size: 2.5rem;

        text-shadow: 2px 2px 3px rgba(0, 0, 0, .5);

        span {
          font-size: 1.5rem;
        }
      }

      &.selected  {
        .list__item__name {
          position: relative;
        }

        .list__item__name::before {
          content: "";
          position: absolute;
          left: -20px;
          top: 3px;
          height: 0;
          width: 0;
          color: white;
          // z-index: ;
          border-top: 10px solid transparent;
          border-bottom: 10px solid transparent;
          border-left: 10px solid white;
        }
      }
    }
  }

  .zoom-enter {
    opacity: 0;
    transform: scale(.25);
  }

  .zoom-enter-active {
    transition: transform .5s ease;
  }

  .zoom-leave-active {
    transform: scale(.25);
    opacity: 0;
    transition: all .4s ease;
  }

  .slide-enter {
    transform: translateY(-100%);
  }

  .slide-enter-active {
    transition: transform .4s ease-out;
  }

  .slide-leave-active {
    transform: translateY(-100%);

    transition: all .4s ease-out;
  }
</style>
