# π» Mapped Type

Mapped Type νμ΅ λ΄μ©

<br />

## π¨π»βπ» Mapped Type

### π Mapped Type κΈ°λ³Έ λ¬Έλ²

- λ§΅λ νμμ map ν¨μλ₯Ό νμμ μ μ©νλ€κ³  μκ°νλ©΄ λλ€.
- λ§΅λ νμμ κΈ°μ‘΄μ μλ νμμ λ°μ μλ mapped type κΈ°λ³Έ λ¬Έλ²μ μ΄μ©ν΄μ μλ‘μ΄ νμμ λ§λλ κ²μ΄λ€.

```ts
  { [ P in K ] : T }
  { [ P in K ] ? : T }
  { readonly [ P in K ] : T }
  { readonly [ P in K ] ? : T }
```

<br />

### π Mapped Type κΈ°λ³Έ μμ 

```ts
type Heroes = "Hulk" | "Capt" | "Thor"; //UnionμΌλ‘ κ°μ νμ λ³μΉ­
type HeroAges = { [K in Heroes]: number };
//μλ‘μ΄ νμμΌλ‘ λ³ν
const ages: HeroAges = {
  Hulk: 33,
  Capt: 100,
  Thor: 1000,
};
```
