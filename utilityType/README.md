# π» Utility Type

Utility Type νμ΅ λ΄μ©

<br />

## π¨π»βπ» Utility Type

### π Partial

- νμ(Partial)νμμ νΉμ  νμμ λΆλΆ μ§ν©μ λ§μ‘±νλ νμμ μ μν  μ μλ€.

```ts
interface Address {
  email: string;
  address: string;
}

type MayHaveEmail = Partial<Address>;
const me: MayHaveEmail = {}; // κ°λ₯
const you: MayHaveEmail = { email: "test@abc.com" }; // κ°λ₯
const all: MayHaveEmail = { email: "capt@hero.com", address: "Pangyo" }; // κ°λ₯
```

<br />

### π Pick

- ν½(Pick)νμμ νΉμ  νμμμ λͺ κ°μ μμ±μ μ ν(pick)νμ¬ νμμ μ μν  μ μλ€.

```ts
interface Produce {
  id: number;
  name: string;
  price: number;
  brand: string;
  storck: number;
}

function displayProductDetail(
  shoppingItem: Pick<Product, "id" | "name" | "price">
) { ... }
```

<br />

### π Omit

- μ€λ°(Omit) νμμ νΉμ  νμμμ μ§μ λ μμ±λ§ μ κ±°ν νμμ μ μν΄ μ€λ€.

```ts
interface AddressBook {
  name: string;
  phone: number;
  address: string;
  company: string;
}
const phoneBook: Omit<AddressBook, "address"> = {
  name: "μ¬νκ·Όλ¬΄",
  phone: 12342223333,
  company: "λ΄ λ°©",
};
const chingtao: Omit<AddressBook, "address" | "company"> = {
  name: "μ€κ΅­μ§",
  phone: 44455557777,
};
```
