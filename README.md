# Vue Lightbox

Vue component that wraps any content into a lightbox popup



## Props

### show
**Type**: _Boolean_  
**Default**: `false`


### bgcolor
**Type**: _String_  
**Default**: `rgba(0,0,0,.9)`

Darkening background color


### noscroll
**Type**: _String_ | _Boolean_  
**Default**: `true`

Blocks vertical scrolling for the `body` tag


### zIndex
**Type**: _Number_  
**Default**: `99999`

Lightbox element `z-index`


### theme
**Type**: _String_  

Addition class for the lightbox instance


## Custom Events

### close

The event is triggered when the 'close' button is pressed



## Usage

```javascript
import Lightbox from './components/vue-lightbox.vue'
Vue.component('VueLightbox', Lightbox);
```

```html
<Lightbox :show="show" @close="show = false">
   <ul>
      <li>001</li>
      <li>002</li>
      <li>003</li>
      <li>004</li>
      <li>005</li>
   </ul>
</Lightbox>
```

Custom close button: 

```css
.custom {
   .close_button {
      background-image: url('my_custom_close.svg');
   }
}
```

You should set `.custom` class through `theme` attribute first.



