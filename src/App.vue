<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Built-In Directives</h1>
                <p v-text="'Some Text'"></p>
                <p v-html="'<strong>Some strong text</strong>'"></p>

            </div>
        </div>
        <hr />
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Custom Directives</h1>
                <p v-highlight:background.delayed="'red'">Color this</p>
                <p v-local-highlight:background.delayed.blink="{mainColor: 'red', secondColor: 'green', delay: 500}">Color this</p>

            </div>
        </div>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Directives Exercise</h1>
                <button v-customOn:click="clicked">Click here!</button>
            </div>

        </div>
        <hr />
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <div
              style="width:100px; height:100px; background-color: lightgreen"
              v-customOn:mouseenter="mouseEntered"
              v-customOn:mouseleave="mouseLeft"
              >
          </div>
        </div>

        <hr />


    </div>
</template>

<script>
    export default {
      methods: {
        clicked(){
          alert('Clicked')
        },
        mouseEntered(){
          console.log('mouse entered');
        },
        mouseLeft(){
          console.log('mouse left');
        }
      },
      directives: {
        customOn: {
          bind(el, binding){
            // el.onclick = function() {
            //   binding.value();
            // }
            const type = binding.arg;
            const fn = binding.value;
            el.addEventListener(type, fn);
          }
        },
        'local-highlight': {
          bind(el, binding){
            var delay = 0;
            if(binding.modifiers['delayed']){
              delay = 3000;
            }
            if(binding.modifiers['blink']){
              let mainColor = binding.value.mainColor;
              let secondColor = binding.value.secondColor;
              let currentColor = mainColor;
              setTimeout(() => {
                setInterval(() => {
                  if(currentColor == secondColor ? currentColor = mainColor : currentColor = secondColor);
                  if(binding.arg == 'background'){
                    el.style.backgroundColor = currentColor;
                  } else {
                    el.style.color = currentColor;
                  }
                }, binding.value.delay);
              }, delay);
            } else {
              setTimeout(() => {
                if(binding.arg == 'background'){
                  el.style.backgroundColor = binding.value.mainColor;
                } else {
                  el.style.color = binding.value.mainColor;
                }
              }, delay);
            }

          }
        }
      }
    }
</script>

<style>

</style>
