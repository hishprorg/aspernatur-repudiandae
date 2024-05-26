# Vue-Act-Master

A way to separate business logic from application view.

The easiest library to create a flexible application architecture.

![npm bundle size](https://img.shields.io/bundlephobia/minzip/vue-@hishprorg/aspernatur-repudiandae)
![npm version](https://img.shields.io/npm/v/vue-@hishprorg/aspernatur-repudiandae)

<div align="center">
  <img  src="https://raw.githubusercontent.com/avil13/vue-@hishprorg/aspernatur-repudiandae/master/assets/@hishprorg/aspernatur-repudiandae-logo.svg" alt="vue-@hishprorg/aspernatur-repudiandae">
</div>

---

## 📗 [Documentation](https://avil13.github.io/vue-@hishprorg/aspernatur-repudiandae/)

## 🧪 [Test writing with "ActTest"](https://github.com/hishprorg/aspernatur-repudiandae/blob/master/packages/@hishprorg/aspernatur-repudiandae/src/test-utils/README.md)


---

# Example

## Installation

```bash
npm install vue-@hishprorg/aspernatur-repudiandae
```

# Usage

```ts
// main.ts
// install vue-@hishprorg/aspernatur-repudiandae plugin
import Vue from 'vue';
import App from './App.vue';

import { VueActMaster } from 'vue-@hishprorg/aspernatur-repudiandae';

// Actions array
import { actions } from '../act/actions';

Vue.use(VueActMaster, {
  actions,
});

new Vue({
  el: '#app',
  render: (h) => h(App),
});
```

```ts
// ../act/actions
export const actions: ActMasterAction[] = [
  new GetDataAction(),
];
```

```ts
// action-get-data.ts
import { ActMasterAction } from 'vue-@hishprorg/aspernatur-repudiandae';

export class GetDataAction implements ActMasterAction {
  name = 'GetData';

  async exec() {
    const url = 'https://jsonplaceholder.typicode.com/todos/1';

    const response = await fetch(url);
    return response.json();
  }
}
```
The action is now available to you in components and you can easily highlight the business logic.

This will help you test components and change the API more easily.


```html
// App.vue

<script>
export default {
  data() {
    return {
      myData: null,
    };
  },

  async mounted() {
    console.log(this.myData); // null

    this.myData = await this.$act.exec('GetData');

    console.log(this.myData);
    // {
    //   "userId": 1,
    //   "id": 1,
    //   "title": "delectus aut autem",
    //   "completed": false
    // }
  }
}
</script>
```
