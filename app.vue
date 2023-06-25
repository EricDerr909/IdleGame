<template>
  <div>
  <pre>
  || ______________________________________________________________________________________ ||
  ||                          ________                   __                                 ||
  ||                          \______ \   __ __   ____  |  | __                             ||
  ||                           |    |  \ |  |  \_/ ___\ |  |/ /                             ||
  ||                           |    `   \|  |  /\  \___ |    \                              ||
  ||                          /_______  /|____/  \___  >|__|_ \                             ||
  ||                                  \/             \/      \/                             ||
  ||                           _____                                                        ||
  ||                          /  _  \  _______   _____   ___.__.                            ||
  ||                         /  /_\  \ \_  __ \ /     \ \   |  |                            ||
  ||                        /    |    \ |  | \/|  Y Y  \ \___  |                            ||
  ||                        \____|__  / |__|   |__|_|  / / ____|                            ||
  ||                                \/               \/  \/                                 ||
  || ______________________________________________________________________________________ ||
  <br/>


    Eggs: {{ eggCount }}          Ducks: {{ duckCount }} <br/>
    <button @click="lay()">Lay Egg</button>           <button @click="hatch()">Hatch Egg</button>

  </pre>
  </div>
</template>

<script setup>
  let eggCount = ref(0);
  let duckCount = ref(1);

  function lay(){
    eggCount.value += duckCount.value;
  }

  function hatch(){
    if(eggCount.value > 0){
      duckCount.value += 1;
      eggCount.value -= 1;
    }
  }
</script>