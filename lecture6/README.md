# ๐ป TypeScript-Lecture-6
6๊ฐ์ ์ฃผ์๋ด์ฉ

<br />

## ๐จ๐ปโ๐ป ๋ฐ๋ณต๊ธฐ ์ดํดํ๊ธฐ
### ๐ ๋ฐ๋ณต๊ธฐ์ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์
- ํ๋ก๊ทธ๋๋ฐ ์ธ์ด๋ง๋ค ์กฐ๊ธ์ฉ ๊ตฌํ ๋ฐฉ์์ด ๋ค๋ฅด๊ธด ํ์ง๋ง, ๋๋ถ๋ถ ํ๋ก๊ทธ๋๋ฐ ์ธ์ด์์ ๋ฐ๋ณต๊ธฐ๋ ๋ค์๊ณผ ๊ฐ์ ํน์ง์ด ์๋ค.
```
  1. next๋ผ๋ ์ด๋ฆ์ ๋ฉ์๋๋ฅผ ์ ๊ณตํ๋ค.
  2. next๋ฉ์๋๋ value์ done์ด๋ผ๋ ๋ ๊ฐ์ ์์ฑ์ ๊ฐ์ง ๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ค.
```

<br />

```ts
  export const createRangeIterable = (from: number, to: number) => {
    let currentValue = from;

    return {
      next() {
        const value = currentValue < to ? currentValue++ : undefined;
        const done = value === undefined; 
        return { value, done };
        // ex {1, false}, {2, false}, {3, false}, {4, true}
      }
    }
  }

  const iterator = createRangeIterable(1, 3 + 1);

  while (true) {
    const { value, done } = iterator.next(); //๋ฐ๋ณต๊ธฐ ๋์

    if(done) break;
    console.log(value); // 1 2 3 
  }
```
- createRangeIterable ํจ์๋ next ๋ฉ์๋๊ฐ ์๋ ๊ฐ์ฒด๋ฅผ ๋ฐํํ๋ฏ๋ก ์ด ํจ์๋ ๋ฐ๋ณต๊ธฐ๋ฅผ ์ ๊ณตํ๋ ์ญํ ์ ํ๋ค. ์ด๋ฅผ `๋ฐ๋ณต๊ธฐ ์ ๊ณต์(iterable)`๋ผ๊ณ  ํ๋ค.
- createRangeIterable ํจ์๋ฅผ ํธ์ถํด ๋ฐ๋ณต๊ธฐ๋ฅผ ์ป๊ณ  iterator ๋ณ์์ ์ ์ฅํ๋ค.
- ๋ฐ๋ณต๊ธฐ๋ ์ด์ฒ๋ผ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์๋ฅผ ํธ์ถํด์ผ๋ง ์ป์ ์ ์๋ค.

<br />

### ๐ ๋ฐ๋ณต๊ธฐ๋ ์ ํ์ํ๊ฐ?
- iterator.next ๋ฉ์๋๊ฐ ๋ฐ๋ณต ํธ์ถ๋  ๋๋ง๋ค ๊ฐ๊ธฐ ๋ค๋ฅธ ๊ฐ์ด ์ถ๋ ฅ๋๋ค. ๋ฐ๋ณต๊ธฐ ์ ๊ณต์๊ฐ ์์ฑํ ๊ฐ 1, 2 , 3์ ๋ฐฐ์ด์ ๋ด์์ ์ถ๋ ฅํ์ง ์๊ณ , ๋ง์น for๋ฌธ์ ๋๋ฉด์ ๊ฐ์ ์ฝ์ ์ถ๋ ฅ๋ฌธ์ผ๋ก ์ฐ์ด๋ธ ๋ฏํ ๋ชจ์ต์ด๋ค.
- ๋ฐ๋ณต๊ธฐ ์ ๊ณต์๋ ์ด์ฒ๋ผ ์ด๋ค ๋ฒ์์ ๊ฐ์ ํ๊บผ๋ฒ์ ๋ฐฐ์ด์ ๋ด์ง ์๊ณ  ๊ฐ์ด ํ์ํ  ๋๋ง๋ค ์์ฑํ๋ค.
```ts
  export const range = (from: number, to: number): number[] => {
    return from < to ? [from, ...range(from + 1, to)] : [];
  }
```
- createRangeIterable ํจ์๋ ๊ฐ์ด ํ์ํ ์์ ์ ๋น๋ก์ ์์ฑํ์ง๋ง, range ํจ์๋ ํ์ํ ์์ ๋ณด๋ค ์ด์ ์ ๋ฏธ๋ฆฌ ์์ฑํ๋ค๋ ์ฐจ์ด๊ฐ ์๋ค.
- ์์คํ ๋ฉ๋ชจ๋ฆฌ์ ํจ์จ์ฑ ๊ด์ ์์ ๋ณด๋ฉด createRangeIterable ํจ์๊ฐ ๋ฉ๋ชจ๋ฆฌ๋ฅผ ํจ์ฌ ์ ๊ฒ ์๋ชจํ๋ค.

<br />

### ๐ for...of๋ฌธ๊ณผ [Symobol.iteraotr] ๋ฉ์๋
- ์์ range ํจ์๋ for...of ๊ตฌ๋ฌธ์ of ๋ค์ ์ฌ ์ ์๋ค.
- ๊ทธ๋ฌ๋ createRangeIterable ํจ์๋ฅผ for...of ๊ตฌ๋ฌธ์ ์ ์ฉํ๋ฉด '[Symobol.iterator]()๋ฉ์๋๊ฐ ์๋ค'๋ ์ค๋ฅ๊ฐ ๋ฐ์ํ๋ค.

```ts
  const iterator = createRangeIterable(1, 3 + 1);
  for(let value of iterable) {
    console..og(value); //์ค๋ฅ ๋ฐ์
  }
```
- ์ฌ๊ธฐ์ ๋ฐ์ํ ์ค๋ฅ๋ createRangeIterable ํจ์๋ฅผ ํด๋์ค๋ก ๊ตฌํํด์ผ ํ๋ค๋ ๊ฒ์ ์๋ฏธํ๋ค.

<br />

```ts
  export class RangeIterable {
    constructor(public from: number, public to: number) {}
    [Symbol.iterator]() {
      const that = this;
      
      let currentValue = that.from;
      
      return {
        next() {
          const value = currentValue < that.to ? currentValue++ : undefined;
          const done = value === undefined; 
          return { value, done };
        }
      }
    }
  }

  const iterator = new RangeIterable(1, 3 + 1);

  console.log(iterator); // RangeIterable { from: 1, to: 4 }

  for(let value of iterator) {
    console.log(value);
  }
```
- ์ฐธ๊ณ  ์ฌํญ์ผ๋ก ํด๋์ค์ ๋ฉ์๋๋ ์๋ฐ์คํฌ๋ฆฝํธ์ function ํค์๋๊ฐ ์๋ต๋์์ ๋ฟ ์ฌ์ค์ function ํค์๋๋ก ๋ง๋ค์ด์ง๋ ํจ์์ด๋ค.
- ๊ทธ๋ฐ๋ฐ function ํค์๋๋ก ๋ง๋ค์ด์ง๋ ํจ์๋ ๋ด๋ถ์์ this ํค์๋๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
- RangeIterable ํด๋์ค์์ this ๊ฐ์ `that ๋ณ์`์ ๋ด๊ณ  ์๋๋ฐ, ์ด๋ next ๋ฉ์๋ ์์ ์๋ `to`๋ฅผ ์ํจ์ด๋ค. next ๋ฉ์๋ ๋ํ function ํค์๋๊ฐ ์๋ต๋ ๋ฉ์๋์ด๋ฏ๋ก ์ปดํ์ผ๋ฌ๊ฐ next์ this๋ก ํด์๋์ง ์๊ฒ ํ๋ ์๋ฐ์คํฌ๋ฆฝํธ์ ์ ๋ชํ ์ฝ๋ ํธ๋ฆญ์ด๋ค.

<br />

### ๐ iterable<T>์ iterator<T> ์ธํฐํ์ด์ค
- ํ์์คํฌ๋ฆฝํธ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์์ `iterable<T>`์ `iterator<T>` ์ ๋ค๋ฆญ ์ธํฐํ์ด์ค๋ฅผ ์ฌ์ฉํ  ์ ์๋ค. 
- `iterable<T>`๋ ๋ค์์ฒ๋ผ ์์ ์ ๊ตฌํํ๋ ํด๋์ค๊ฐ `[Symobol.iteraotr]`๋ฉ์๋๋ฅผ ์ ๊ณตํ๋ค๋ ๊ฒ์ ๋ชํํ๊ฒ ์๋ ค์ฃผ๋ ์ญํ ์ ํ๋ค.
```
  class ๊ตฌํ ํด๋์ค implements Iterable<์์ฑํ  ๊ฐ์ ํ์> {}
```
- ๋ํ, `Iterator<T>`๋ ๋ฐ๋ณต๊ธฐ๊ฐ ์์ฑํ  ๊ฐ์ ํ์์ ๋ช์ํด์ค๋ค.
```
  [Symobol.iteraotr](): Iterator<์์ฑํ  ๊ฐ์ ํ์> {}
```

<br />

```ts
  export class StringIterable implements Iterable<string> {
    constructor(private strings: string[], private currentIndex: number = 0) {}

    [Symbol.iterator](): Iterator<string> {
      const that = this;

      let currentIndex = that.currentIndex;
      let length = that.strings.length;

      const iterator: Iterator<string> = {
        next(): { value: string, done: boolean } {
          const value = currentIndex < length ? that.strings[currentIndex++]: 'undefined';
          const done = value === 'undefined';

          return { value, done};
        }
      }
      return iterator;
    }
  }

  const IterableValue = new StringIterable(['hello', 'world', '!']);

  console.log(IterableValue); 
  //StringIterable { strings: [ 'hello', 'world', '!' ], currentIndex: 0 }

  for(let value of new StringIterable(['hello', 'world', '!'])) {
    console.log(value); //hello world !
  }
```

<br />

## ๐จ๐ปโ๐ป ์์ฑ๊ธฐ ์ดํดํ๊ธฐ
- ESNext(ES6 ์ด์) ์๋ฐ์คํฌ๋ฆฝํธ์ ํ์์คํฌ๋ฆฝํธ๋ `yield`๋ผ๋ ํค์๋๋ฅผ ์ ๊ณตํ๋ค. yield๋ ๋ง์น return ์ฒ๋ผ ๊ฐ์ ๋ฐํํ๋ค.
- yield๋ `function*` ํค์๋๋ฅผ ์ฌ์ฉํ ํจ์์์๋ง ํธ์ถํ  ์ ์๋ค.
- `function*` ํค์๋๋ก ๋ง๋  ํจ์๋ฅผ `์์ฑ๊ธฐ(generator)`๋ผ๊ณ  ํ๋ค.
```ts
  export function* generator() {
    console.log('generator started...');
    
    let value = 1;
    while(value < 4) {
      yield value++;
    }
    console.log('generator finished...');
  }

  for(let value of generator()) {
    console.log(value);
    /*
      ์ถ๋ ฅ
      generator started...
      1
      2
      3
      generator finished...
    */
  }
```

<br />

### ๐ function* ํค์๋
- generator ํจ์๋ ์ง๊ธ๊น์ง ๋ณธ ํจ์์ ๋น๊ตํ์ ๋ ๋ค์ ๋ ๊ฐ์ง ์ฐจ์ด๊ฐ ์๋ค.
```
  1. function* ํค์๋๋ก ํจ์๋ฅผ ์ ์ธํ๋ค.
  2. ํจ์ ๋ชธํต ์์ yield๋ฌธ์ด ์๋ค.
```
- ์ฆ function* ํค์๋๋ก ์ ์ธ๋ ํจ์๊ฐ ์์ฑ๊ธฐ์ธ๋ฐ, ์์ฑ๊ธฐ๋ ์ค์ง function* ํค์๋๋ก ์ ์ธํด์ผ ํ๋ฏ๋ก ํ์ดํ ํจ์๋ก๋ ์์ฑ๊ธฐ๋ฅผ ๋ง๋ค ์ ์๋ค.
- ์์ฑ๊ธฐ๋ ๋ฐ๋ณต๊ธฐ๋ฅผ ์ ๊ณตํ๋ `๋ฐ๋ณต๊ธฐ ์ ๊ณต์`๋ก ๋์ํ๋ค.

<br />

### ๐ yield ํค์๋
- ์์ฑ๊ธฐ ํจ์ ์์์๋ yield ํจ์๋ฅผ ์ฌ์ฉํ  ์ ์๋ค. yield๋ `์ฐ์ฐ์(operator)`ํํ๋ก ๋์ํ๋ฉฐ ๋ ๊ฐ์ง ๊ธฐ๋ฅ์ ํ๋ค.
```
  1. ๋ฐ๋ณต๊ธฐ๋ฅผ ์๋์ผ๋ก ๋ง๋ค์ด ์ค๋ค.
  2. ๋ฐ๋ณต๊ธฐ ์ ๊ณต์ ์ญํ ๋ ์ํํ๋ค.
```

<br />

```ts
  export function* rangeGenerator(from: number, to: number) {
    let value = from;
    while(value < to) {
      yield value++;
    }
  }

  let iterator = rangeGenerator(1, 3 + 1);

  while (true) {
    const { value, done } = iterator.next();

    if (done) break;
    console.log(value);
  }

  for(let value of rangeGenerator(4, 6 + 1)) {
    console.log(value);
  }
```
- ์ ์ฝ๋๋ ์์ ๋ณธ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์ ๊ด๋ จ ์ฝ๋์ ํฌ๊ฒ ๋ค๋ฅด์ง ์๋๋ค.

<br />

### ๐ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์์ ๋ฉ์๋๋ก ๋์ํ๋ ์์ฑ๊ธฐ ๊ตฌํ
- ์์ฑ๊ธฐ(generator)๋ ๋ฐ๋ณต๊ธฐ๋ฅผ ์ ๊ณตํ๋ ๋ฐ๋ณต๊ธฐ ์ ๊ณต์๋ก์ ๋์ํ๋ฏ๋ก, ์์ฑ๊ธฐ๋ฅผ ์ฌ์ฉํ๋ฉด StringIterable ํด๋์ค๋ฅผ ๊ฐ๊ฒฐํ๊ฒ ๊ตฌํํ  ์ ์๋ค.
```ts
  export class IterableUsingGenerator<T> implements Iterable<T> {
    constructor(private values: T[] = [], private currentIndex: number = 0) {}

    [Symbol.iterator] = function* () {
      while(this.currentIndex < this.values.length) {
        yield this.values[this.currentIndex++];
      }
    }
  }
```

<br />

### ๐ yield* ํค์๋
- ํ์์คํฌ๋ฆฝํธ๋ yield ํค์๋ ๋ค์ *๋ฅผ ๋ถ์ธ `yield*` ํค์๋๋ ์ ๊ณตํ๋ค. yield๋ ๋จ์ํ ๊ฐ์ ๋์์ผ๋ก ๋์ํ์ง๋ง, `yield*`๋ ๋ค๋ฅธ ์์ฑ๊ธฐ๋ ๋ฐฐ์ด์ ๋์์ผ๋ก ๋์ํ๋ค.
```ts
  function* gen12() {
    yield 1;
    yield 2;
  }

  function* gen12345() {
    yield* gen12();
    yield* [3, 4];
    yield 5;
  }

  for(let value of gen12345()) {
    console.log(value);
  }
```

<br />

### ๐ yield ๋ฐํ ๊ฐ
- yield ์ฐ์ฐ์๋ ๊ฐ์ ๋ฐํํ๋ค.
```ts
  export function* gen() {
    let count = 5;
    let select = 0;
    
    while(count--) {
      select = yield `you select ${select}`;
    }
  }

  const random = (max: number, min: number = 0) => Math.round(Math.random() * (max - min)) + min;
  const iter = gen();

  while(true) {
    const { value, done } = iter.next(random(10, 1));
    
    if(done) break;
    console.log(value);
  }
```
- yield ์ฐ์ฐ์์ ๋ฐํ๊ฐ์ ๋ฐ๋ณต๊ธฐ์ next ๋ฉ์๋ ํธ์ถ ๋ ๋งค๊ฐ๋ณ์์ ์ ๋ฌํ๋ ๊ฐ์ด๋ค.
- ์ ์ฝ๋ ์คํ ๊ฒฐ๊ณผ๋ ์ด์ ์ next ๋ฉ์๋๊ฐ ์ ๋ฌํ ๊ฐ์ด ๋ค์ gen ํจ์์ ๋ด๋ถ ๋ก์ง์ ์ํด ํ์ฌ์ value ๊ฐ์ด ๋์ด ์ถ๋ ฅ๋๋ค.