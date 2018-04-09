<template>
    <div class="add">
      <div class="input-container">
          <vue-google-autocomplete
            id="input"
            placeholder="Enter city name"
            types="(cities)"
            @blur="onBlur"
            @placechanged="placeChanged" >
          </vue-google-autocomplete>
      </div>
    </div>
</template>

<script>
  import VueGoogleAutocomplete from 'vue-google-autocomplete'

  export default {
    components: {
      VueGoogleAutocomplete
    },
    data: function () {
      return {
      }
    },
    methods: {
      close: function () {
        this.$emit('close')
      },
      onBlur: function () {
        // Do something here
      },
      placeChanged: function (address, placeResult, id) {
        var name = ''
        if (address.locality) {
          name = address.locality
        } else {
          name = placeResult.name
        }

        this.$emit('cityAdded', {
          name: name,
          utc_offset: placeResult.utc_offset
        })
        setTimeout(() => {
          this.close()
        }, 250)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .add {
    display: block;
    height: 100vh;
    // background-color: #27203F;
    background-color: #3e3e3e;
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;

    display: flex;
    flex-direction: column;
  }

  .input-container {
    padding: 2rem;
    width: 100%;

    input {
      color: white;
      font-size: 2.5rem;
      display: block;
      margin-left: 40px;
      width: 80%;

      position: relative;

      border: none;
      font-size: 1.5rem;
      background-color: transparent;

      border-bottom: 1px solid rgba(255, 255, 255, .5);
      padding: 0 0 5px 0;

      &:focus {
        outline: none;
      }
    }
  }
</style>
