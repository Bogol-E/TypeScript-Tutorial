# π» TypeScript-Lecture-5
5κ°μ μ£Όμλ΄μ©

<br />

## π¨π»βπ» λ°°μ΄ μ΄ν΄νκΈ°
### π μλ°μ€ν¬λ¦½νΈμμ λ°°μ΄μ κ°μ²΄λ€
- μλ°μ€ν¬λ¦½νΈμμ λ°°μ΄μ λ€λ₯Έ μΈμ΄μ λ€λ₯΄κ² κ°μ²΄μ΄λ€.
- λ°°μ΄μ Array ν΄λμ€μ μΈμ€ν΄μ€μΈλ°, ν΄λμ€μ μΈμ€ν΄μ€λ κ°μ²΄μ΄κΈ° λλ¬Έμ΄λ€.

<br />

### π λ°°μ΄μ νμ
- νμμ€ν¬λ¦½νΈμμ λ°°μ΄μ νμμ `μμ΄ν νμ[]`μ΄λ€.
- μλ₯Ό λ€μ΄, λ°°μ΄μ μμ΄νμ΄ `number`νμμ΄λ©΄ λ°°μ΄μ νμμ `number[]`μ΄κ³ , μμ΄νμ΄ `string`νμμ΄λ©΄ `string[]`μ΄λ€.
```js
  let numArray: number[] = [1, 2, 3];
  let strArray: string[] = ['Hello', 'World'];

  type IPerson = {
    name: string;
    age?: number;
  }

  let personArray: IPerson[] = [{ name: 'Jack' }, { name: 'Jeon', age: 32 }];
  
  console.log(personArray); //[{ name: 'Jack' }, { name: 'Jeon', age: 32 }]
```

<br />

### π λ¬Έμμ΄κ³Ό λ°°μ΄ κ° λ³ν
- νμμ€ν¬λ¦½νΈμμλ λ¬Έμ νμμ΄ μκ³  λ¬Έμμ΄μ λ΄μ© λν λ³κ²½ν  μ μλ€. μ΄λ¬ν νΉμ§ λλ¬Έμ λ¬Έμμ΄μ κ°κ³΅νλ €λ©΄ λ¨Όμ  λ¬Έμμ΄μ λ°°μ΄λ‘ μ νν΄μΌ νλ€.
- λ³΄ν΅ λ¬Έμμ΄μ λ°°μ΄λ‘ μ νν  λλ `String`ν΄λμ€μ `split` λ©μλλ₯Ό μ¬μ©νλ€.
- `split`λ©μλλ λ¬Έμμ΄μ μͺΌκ°λ κΈ°μ€μ΄ `κ΅¬λΆμ(delimiter)`λ₯Ό μλ ₯λ°μ λ¬Έμμ΄μ `string[]`λ°°μ΄λ‘ λ§λ€μ΄ μ€λ€.
```ts
  const split = (str: string, delim: string = ''): string[] => str.split(delim);

  console.log(split('hello')); //[ 'h', 'e', 'l', 'l', 'o' ]
  console.log(split('h_e_l_l_o', '_')); //[ 'h', 'e', 'l', 'l', 'o' ]
```

<br />

- `join` ν¨μλ λ§€κ° λ³μλ‘ μ λ¬λ°μ `string[]` νμ λ°°μ΄κ³Ό κ΅¬λΆμλ₯Ό μ΄μ©ν΄ `String`ν΄λμ€μ `join`λ©μλλ₯Ό νΈμΆν¨μΌλ‘μ¨ λ¬Έμμ κ΅¬λΆμλ₯Ό κ²°ν©ν μ λ¬Έμμ΄μ λ°ννλ€.
```ts
  const join = (strArray: string[], delim: string = ''): string => strArray.join(delim);

  console.log(join(['h', 'e', 'l', 'l', 'o'])); 
  console.log(join(['h', 'e', 'l', 'l', 'o'], '_'));
```

<br />

### π μΈλ±μ€ μ°μ°μ
```ts
  const numbers: number[] = [1, 2, 3, 4, 5];
  
  for (let i = 0; i < numbers.length; i++) {
    const item: number = numbers[i];
    console.log(item);
  }
```

<br />

### π μ λ€λ¦­ λ°©μ νμ
- λ°°μ΄μ λ€λ£¨λ ν¨μλ₯Ό μμ±ν  λλ `number[]`μ κ°μ΄ νμμ΄ κ³ μ λ ν¨μλ₯Ό λ§λ€κΈ°λ³΄λ€λ `T[]`ννλ‘ λ°°μ΄μ μμ΄ν νμμ νκΊΌλ²μ νννλ κ²μ΄ νΈλ¦¬νλ€.
- νμμ `T`μ κ°μ μΌμ’μ λ³μλ‘ μ·¨κΈνλ κ²μ `μ λ€λ¦­(Generics)νμ` μ΄λΌκ³  νλ€.
- `number[]`, `string[]`, `IPerson[]` λ± λ€μν μμ΄ν νμμ κ°μ§λ λ°°μ΄μ λκ°μ΄ μ μ©λκ² νλ €λ©΄ λ€μμ²λΌ λ°°μ΄μ νμ μ£Όμμ `T[]`λ‘ νννλ€.
```ts
  const arrayLength = (array: T[]): number => array.length;
```
- μμ κ°μ μ½λλ‘ μ§λ©΄ `μ»΄νμΌλ¬`κ° `T`μ μλ―Έλ₯Ό μ μ μμ΄μΌ νλ€. μ¦, `T`κ° `νμ λ³μ(type variable)`λΌκ³  μλ €μ€μΌ νλ€.

<br />

```ts
  const arrayLength = <T>(array: T[]): number => array.length;
  const isEmpty = <T>(array: T[]): boolean => arrayLength<T>(array) === 0;

  let numArray: number[] = [1, 2, 3];
  let strArray: string[] = ['Hello', 'World'];

  type IPerson = { 
    name: string;
    age?: number; 
  }

  let PersonArray: IPerson[] = [{ name: 'Jack' }, { name: 'Jeon', age: 32 }];

  console.log(arrayLength(numArray));
  console.log(arrayLength(strArray));
  console.log(arrayLength(PersonArray));
  console.log(isEmpty([]));
  console.log(isEmpty([1]));
```

<br />

### π μ λ€λ¦­ ν¨μμ νμ μΆλ‘ 
```ts
  const identity = <T>(n: T): T => n;

  console.log(identity<boolean>(true)); //true
  console.log(identity(true)); //true
```
- λ³΄ν΅ μ λ€λ¦­ ννλ‘ κ΅¬νλ ν¨μλ μμΉμ μΌλ‘λ `identity<boolean>(true)`μ²λΌ `νμ λ³μ`λ₯Ό λ€μκ³Ό κ°μννλ‘λͺμν΄ μ£Όμ΄μΌ νλ€.
- νμ§λ§ νμμ€ν¬λ¦½νΈλ νμ λ³μ λΆλΆμ μλ΅ν  μ μκ² νλ€. νμμ€ν¬λ¦½νΈλ νμ λ³μκ° μλ΅λ μ λ€λ¦­ ν¨μλ₯Ό λ§λλ©΄ `νμ μΆλ‘ `μ ν΅ν΄ μλ΅λ νμμ μ°ΎμλΈλ€.

<br />

## π¨π»βπ» λ°°μ΄μ filter, map, reduce,
### π filter
- filter λ©μλλ `μ½λ°± ν¨μ`μ κ²°κ³Ό κ°μ `true`λ‘ λ§λλ μμλ€λ‘λ§ κ΅¬μ±λ `λ³λμ λ°°μ΄`μ λ°ννλ€. 
```ts
  filter(callback: (value: T, index?: number): boolean): T[];
```
```ts
  const numList: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

  let odd: number[] = numList.filter(value => value % 2 !== 0); 
  let even: number[] = numList.filter(value => value % 2 === 0); 

  console.log(odd); //[ 1, 3, 5, 7, 9 ]
  console.log(even); //[ 2, 4, 6, 8, 10 ]
```

<br />

### π map
- λ°°μ΄μ κ° μμλ³λ‘ μ§μ λ ν¨μλ₯Ό μ€νν κ²°κ³Όλ‘ κ΅¬μ±λ `μλ‘μ΄ λ°°μ΄`μ `λ°ν`νλ€.
- forEachμ λΉμ·νκ² μλνμ§λ§ forEachλ μλ‘μ΄ λ°°μ΄μ λ°ννμ§ μμ.
- map λ©μλλ filterμ λ€λ₯΄κ² μλ ₯ νμκ³Ό λ€λ₯Έ νμμ λ°°μ΄μ λ§λ€ μ μλ€.
```ts
  map(callback: (value: T, index?: number): Q): Q[];
```
```ts
  let squers: number[] = [1, 2, 3, 4, 5]

  squers = squers.map((value:number) => value * value);

  console.log(squers); //[ 1, 4, 9, 16, 25 ]
```

<br />

### π reduce
- `λμ°κΈ°(accumulator)`λ° `λ°°μ΄μ κ° κ°(μ’μμ μ°)`μ λν΄ (λμ°λ)`ν κ°`μΌλ‘ μ€λλ‘ ν¨μλ₯Ό μ μ©
```ts
  reduce(callback: (result: T, value: T), initialValue: T): T
```
```ts
  let reduceSum: number = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    .reduce((result: number, value: number) => result + value);

  console.log(reduceSum); //55
```

<br />

## π¨π»βπ» μμ ν¨μμ λ°°μ΄
### π μμ ν¨μ
- μμ ν¨μλ `λΆμ ν¨κ³Ό(side-effect)`κ° μλ ν¨μλ₯Ό λ§νλ€.
- λΆμ ν¨κ³Όλ ν¨μκ° κ°μ§ κ³ μ ν λͺ©μ  μ΄μΈμ λ€λ₯Έ ν¨κ³Όκ° λνλλ κ²μ μλ―Ένλ©° `λΆμμ©`μ΄λΌκ³  νλ€.
- λΆμ ν¨κ³Όκ° μλ ν¨μλ `λΆμ ν¨μ(impure function)`λΌκ³  νλ€.
- λ€μμ μμ ν¨μμ μ‘°κ±΄μ΄λ€.
```
  1. ν¨μ λͺΈν΅μ μμΆλ ₯ κ΄λ ¨ μ½λκ° μμ΄μΌ νλ€.
  2. ν¨μ λͺΈν΅μλ λ§€κ° λ³μ κ°μ λ³κ²½μν€μ§ μλλ€.(μ¦, constλ readonly ννλ‘λ§ μ¬μ©νλ€)
  3. ν¨μλ λͺΈν΅μμ λ§λ€μ΄μ§ κ²°κ³Όλ₯Ό μ¦μ λ°ννλ€.
  4. ν¨μ λ΄λΆμ μ μ­ λ³μλ μ μ  λ³μλ₯Ό μ¬μ©νμ§ μλλ€.
  5. ν¨μκ° μμΈλ₯Ό λ°μμν€μ§ μλλ€.
  6. ν¨μκ° μ½λ°± ν¨μλ‘ κ΅¬νλμκ±°λ ν¨μ λͺΈν΅μ μ½λ°± ν¨μλ₯Ό μ¬μ©νλ μ½λκ° μλ€.
  7. ν¨μ λͺΈν΅μ Promiseμ κ°μ λΉλκΈ° λ°©μμΌλ‘ λμνλ μ½λκ° μλ€.
```

<br />

### π κΉμ λ³΅μ¬μ μμ λ³΅μ¬
- νλ‘κ·Έλλ° μΈμ΄μμ μ΄λ€ λ³μ«κ°μ λ€λ₯Έ λ³μ«κ°μΌλ‘ μ€μ νλ κ²μ λ³΅μ¬(copy)λΌκ³  νννλ€.
- λ³΅μ¬μλ `κΉμ λ³΅μ¬(deep-copy`μ `μμ λ³΅μ¬(shallow-copy)` λ μ’λ₯κ° μλ€.
- μμ ν¨μλ₯Ό κ΅¬νν  λ λ§€κ°λ³μκ° `λΆλ³μ±μ μ μ§`ν΄μΌ νλ―λ‘, λ§€κ°λ³μλ₯Ό κ°κ³΅νλ €κ³  ν  λ `κΉμ λ³΅μ¬`λ₯Ό μ€νν΄ λ§€κ° λ³μ κ°μ΄ λ³κ²½λμ§ μκ² ν΄μΌ νλ€.
- κΉμ λ³΅μ¬λ λμ λ³μ κ°μ΄ λ°λ λ `μλ³Έ λ³μ κ°μ κ·Έλλ‘μΈ ννλ‘ λμ`νλ€.

<br />

### π μ κ° μ°μ°μμ κΉμ λ³΅μ¬
- λ°°μ΄μμ `μ κ° μ°μ°μ(...)`λ₯Ό μ¬μ©ν΄ λ°°μ΄μ λ³΅μ¬νλ©΄ κΉμ λ³΅μ¬λ₯Ό ν  μ μλ€.
```ts
  const oArray: number[] = [1, 2, 3, 4];
  const deepCopiedArray: number[] = [...oArray];
  deepCopiedArray[0] = 0;
  console.log(oArray, deepCopiedArray) //[1, 2, 3, 4] [0, 2, 3, 4]
```

<br />

- Arrayν΄λμ€λ sortλ©μλλ₯Ό μ κ³΅νλ€. κ·Έλ°λ° sort λ©μλλ μλ³Έ λ°°μ΄μ λ΄μ©μ λ³κ²½νλ€.
```ts
  export const pureSort = <T>(array: readonly T[]): T[] => {
    let deepCopied = [...array];
    return deepCopied.sort();
  }

  let beforeSort: number[] = [6, 2, 9, 0];
  const afterSort = pureSort<number>(beforeSort);

  console.log(beforeSort, afterSort); //[ 6, 2, 9, 0 ] [ 0, 2, 6, 9 ]
```
- λ€μ `pustSort ν¨μ`λ readonly νμμΌλ‘ μλ ₯ λ°°μ΄μ λ΄μ©μ μ μ§ν μ± μ λ ¬ν  μ μλλ‘ `μ κ° μ°μ°μ`μ κΉμ λ³΅μ¬ κΈ°λ₯μ μ¬μ©νλ€.

<br />

## π¨π»βπ» νν
- μλ°μ€ν¬λ¦½νΈμμλ ννμ΄ μμΌλ©° λ¨μν λ°°μ΄μ ν μ’λ₯λ‘ μ·¨κΈλλ€.
- `any[]`μ ννλ νμμ€ν¬λ¦½νΈμ νμ κΈ°λ₯μ λ¬΄λ ₯ννλ―λ‘, νμμ€ν¬λ¦½νΈλ ννμ νμ νκΈ°λ²μ λ°°μ΄κ³Ό λ€λ₯΄κ² μ μΈνλ€.
```ts
  const array: number[] = [1, 2, 3, 4];
  const tuple: [boolean, string] = [true, 'thje result is ok'];
```

<br />

- λ³΄ν΅ ννμ μ¬μ©ν  λλ `νμ λ³μΉ­(alias)`μΌλ‘ ννμ μλ―Έλ₯Ό λͺννκ² νλ€.
- μλ₯Ό λ€μ΄, `[boolean, string]`μ΄λΌκ³  νμμ μ§μ νλ κ²λ³΄λ€ λ€μ μ²λΌ νμ λ³μΉ­μ μ¬μ©ν΄ μ΄ ννμ΄ μ΄λ€ μ©λλ‘ μ¬μ©λλμ§ μ’ λ λΆλͺνκ² μλ €μ£Όλ κ²μ΄ μ’λ€.
```ts
  type ResultType =[boolean, string];

  const array: number[] = [1, 2, 3, 4];
  const tuple: ResultType = [true, 'the result is ok'];
```

<br />