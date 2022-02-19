# asyncData() 에 대하여

# AsyncData란?

페이지의 컴포넌트가 그려지기 전에 서버사이드에서 넘어온 데이터를 페이지에 우겨넣는다고 생각하자

컴포넌트가 그려지기 전이기 때문에 지금까지 vue에서 해왔듯 this. 를 사용하여 내부 접근이 불가능하다

원래대로 였다면 axios를 사용해 데이터를 불러오는 코드가 아래와 같았을 것이다

```jsx
<template>
  <div>
    <p>im index</p>
    <div>
      {{ products }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      products: [],
    };
  },
  async created() {
    const response = await axios.get('http://localhost:3000/products');
    this.products = response.data;
  },
};
</script>
```

nuxt에서는 위 코드대로도 사용할 수는 있지만 권장되지 않는다. 일단 깜빡임이 발생하는 문제도 있기때문

그럼 어떻게 해야할까?

nuxt에서 데이터의 처리는 asyncData()를 사용하여 아래와 같이 한다

```jsx
<template>
  <div>
    <p>im index</p>
    <div>
      {{ products }}
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'IndexPage',
  async asyncData() {
    const response = await axios.get('http://localhost:3000/products');
    const products = response.data;

    return { products };
  },
};
</script>
```

# 주의점

asyncData()는 pages아래 vue 파일에서만 작동한다.

컴포넌트나 layout레벨에서 사용하려고 하면 에러가 날 것이다
