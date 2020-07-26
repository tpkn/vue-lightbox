<!-- Vue Lightbox, http://tpkn.me/ -->
<template>
   <transition name="expand" mode="out-in" appear>
      <div v-if="expanded" :class="[ 'vue-lightbox', theme ]" :style="{ 'z-index': zIndex }">
         <div @click="close" class="bg" :style="{ 'background-color': bgcolor }"></div>
         
         <transition name="collapse" mode="out-in" appear>
            <div class="content">
               <slot></slot>
            </div>
         </transition>

         <div @click="close" class="close_button"></div>
      </div>
   </transition>
</template>
<script>

   export default {
      name: 'Lightbox',

      props: {
         show: {},

         bgcolor: {
            default: 'rgba(0,0,0,.9)'
         },

         zIndex: {
            default: 99999
         },

         noscroll: {
            default: true
         },

         theme: {}
      },

      data: () => {
         return {
            expanded: false,
         }
      },

      methods: {
         close(n){
            this.expanded = !this.expanded;
            this.$emit('close');
         }
      },

      beforeMount(){
         this.expanded = this.show;
      },

      watch: {
         show: {
            immediate: true,
            handler: function(after){
               this.expanded = after;
            }
         },

         expanded: {
            immediate: true,
            handler: function(after){
               if(this.noscroll){
                  let body_style = document.body.style;
                  if(after){
                     body_style.position = 'fixed';
                     body_style.overflow = 'hidden';
                  }else{
                     body_style.position = 'static';
                     body_style.overflow = 'auto';
                  }
               }
            }
         }
      }
   }

</script>
<style lang="scss" scoped>

   .vue-lightbox {
      position: fixed;
      left: 0; right: 0; top: 0; bottom: 0;
      overflow: hidden;

      .bg {
         position: absolute;
         left: 0; right: 0; top: 0; bottom: 0;
      }

      .content {
         position: absolute;

         left: 0;
         right: 0;
         top: 0;
         bottom: 0;
         margin: auto 0;

         overflow-y: auto;
         -webkit-overflow-scrolling: touch;
      }

      .close_button {
         position: absolute;

         right: 0;
         top: 0;

         width: 40px;
         height: 40px;

         background-image: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZlcnNpb249IjEuMSIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHByZXNlcnZlQXNwZWN0UmF0aW89Im5vbmUiIHg9IjBweCIgeT0iMHB4IiB3aWR0aD0iNzhweCIgaGVpZ2h0PSI3OHB4IiB2aWV3Qm94PSIwIDAgNzggNzgiPg0KCTxkZWZzPg0KCQk8cGF0aCBpZD0iU3ltYm9sXzFfMF9MYXllcjBfMF8xX1NUUk9LRVMiIHN0cm9rZT0iI2ZmZmZmZiIgc3Ryb2tlLXdpZHRoPSI1IiBzdHJva2UtbGluZWpvaW49InJvdW5kIiBzdHJva2UtbGluZWNhcD0icm91bmQiIGZpbGw9Im5vbmUiIGQ9Ig0KTSAwIDg5DQpMIDAgMCAtODkgMA0KTSAwIC04OQ0KTCAwIDAgODkgMCIgLz4NCgk8L2RlZnM+DQoJPGcgdHJhbnNmb3JtPSJtYXRyaXgoIDAuMjE5MDI0NjU4MjAzMTI1LCAwLjIxOTAyNDY1ODIwMzEyNSwgLTAuMjE5MDI0NjU4MjAzMTI1LCAwLjIxOTAyNDY1ODIwMzEyNSwgMzkuMiwzOS4yKSAiPg0KCQk8ZyB0cmFuc2Zvcm09Im1hdHJpeCggMSwgMCwgMCwgMSwgMCwwKSAiPg0KCQkJPHVzZSB4bGluazpocmVmPSIjU3ltYm9sXzFfMF9MYXllcjBfMF8xX1NUUk9LRVMiIC8+DQoJCTwvZz4NCgk8L2c+DQo8L3N2Zz4NCg==');
         background-position: 0 0;
         background-repeat: no-repeat;
         background-size: contain;

         transform-origin: 50% 50%;
         transition: transform .3s ease-out;

         cursor: pointer;
      }

      .close_button:hover {
         transform: scale(1.1);
      }
   }


   .expand-enter-active {
      transition: opacity .4s cubic-bezier(0.490, 0.265, 0.450, 1);
   }
   .expand-leave-active {
      transition: opacity .2s cubic-bezier(0.490, 0.265, 0.450, 1);
   }
   .expand-enter, .expand-leave-to {
      opacity: 0;
   }


   .collapse-enter-active {
      transition: opacity .4s cubic-bezier(0.490, 0.265, 0.450, 1) .2s;
   }
   .collapse-leave-active {
      transition: opacity .2s cubic-bezier(0.490, 0.265, 0.450, 1);
   }
   .collapse-enter, .collapse-leave-to {
      opacity: 0;
   }

</style>
