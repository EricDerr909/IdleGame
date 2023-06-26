<template>
  <div>
    <pre>
  =|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|
  |=                                                                                        =|
  =|                          ________                   __                                 |=
  |=                          \______ \   __ __   ____  |  | __                             =|
  =|                           |    |  \ |  |  \_/ ___\ |  |/ /                             |=
  |=                           |    `   \|  |  /\  \___ |    \                              =|
  =|                          /_______  /|____/  \___  >|__|_ \                             |=
  |=                                  \/             \/      \/                             =|
  =|                           _____                                                        |=
  |=                          /  _  \  _______   _____   ___.__.                            =|
  =|                         /  /_\  \ \_  __ \ /     \ \   |  |                            |=
  |=                        /    |    \ |  | \/|  Y Y  \ \___  |                            =|
  =|                        \____|__  / |__|   |__|_|  / / ____|                            |=
  |=                                \/               \/  \/                                 =|
  =|                                                                                        |=
  |=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=|=
  <br/>
    Ticks: {{ tick }}

    Eggs: {{ eggCount }}
    <button @click="lay()">Lay Egg</button>

    Ducks: {{ duckCount }}
    <button @click="hatch()">Hatch Egg</button>

    Money: ${{ money }}
    Egg Value: ${{ eggValue }}
    <button @click="sell()">Sell Eggs</button>

    Incubators: {{ incubatorCount }}
    Incubator Cost: ${{ incubatorCost }}
    <button @click="buyIncubator()">Buy Incubator</button>

    Egg Pickers: {{ eggPickerCount }}
    Egg Picker Cost: ${{ eggPickerCost }}
    <button @click="buyEggPicker()">Buy Egg Picker</button>

    War Crimes Comitted: {{ warCrimeCount }}
    <button @click="warCrimeComitted()">Commit a War Crime</button>

    Jacobs: {{ jacobCount }}
    <button @click="buyJacob()">Buy a Jacob</button>

    </pre>
  </div>
</template>

<script setup>
  document.body.style.backgroundColor = "Purple"

  let tick = ref(0);
  let eggCount = ref(0);
  let duckCount = ref(1);
  let money = ref(0.0);
  let eggValue = ref(0.05);
  let incubatorCount = ref(0);
  let incubatorCost = ref(100);
  let eggPickerCount = ref(0);
  let eggPickerCost = ref(100);
  let warCrimeCount = ref(0);
  let jacobCount = ref(0);

  function tickHappen(){
    tick.value += 1;

    if((tick.value % 5) == 0){
      if(eggCount.value >= incubatorCount.value){
        duckCount.value += incubatorCount.value;
        eggCount.value -= incubatorCount.value;
      }else{
        duckCount.value += eggCount.value;
        eggCount.value = 0;
      }

      if(eggPickerCount.value > duckCount.value){
        eggCount.value += duckCount.value;
      }else{
        eggCount.value += eggPickerCount.value;
      }
    }

    warCrimeCount.value += jacobCount.value;

    jacobCount.value += jacobCount.value;

    setTimeout(tickHappen, 200);
  }

  tickHappen();

  function lay(){
    eggCount.value += duckCount.value;
  }

  function hatch(){
    if(eggCount.value > 0){
      duckCount.value += 1;
      eggCount.value -= 1;
    }
  }

  function sell(){
    money.value = Math.round(((money.value +(eggCount.value * eggValue.value)) + Number.EPSILON) * 100) / 100;
    eggCount.value = 0;
  }

  function buyIncubator(){
    if(incubatorCost.value <= money.value){
      money.value = Math.round(((money.value - incubatorCost.value) + Number.EPSILON) * 100) / 100;
      incubatorCount.value += 1;
      incubatorCost.value = Math.round(((incubatorCost.value * 1.5) + Number.EPSILON) * 100) / 100;
    }
  }

  function buyEggPicker(){
    if(eggPickerCost.value <= money.value){
      money.value = Math.round(((money.value - eggPickerCost.value) + Number.EPSILON) * 100) / 100;
      eggPickerCount.value += 1;
      eggPickerCost.value = Math.round(((eggPickerCost.value * 1.5) + Number.EPSILON) * 100) / 100;
    }
  }

  function warCrimeComitted(){
    warCrimeCount.value += 1;
  }

  function buyJacob(){
    jacobCount.value += 1;
  }

</script>