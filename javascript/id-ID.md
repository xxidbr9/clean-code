# Javascript Clean Code Bahasa Indonesia{

## Daftar Isi

1. [Tipe Data](#tipe-data)
1. [Reference](#references)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Destructuring](#destructuring)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Arrow Functions](#arrow-functions)
1. [Classes & Constructors](#classes--constructors)
1. [Modules](#modules)
1. [Iterators and Generators](#iterators-and-generators)
1. [Properti](#properties)
1. [Variables](#variables)
1. [Hoisting](#hoisting)
1. [Operators & Equality](#comparison-operators--equality)
1. [Blocks](#blocks)
1. [Control Statements](#control-statements)
1. [Comments](#comments)
1. [Whitespace](#whitespace)
1. [Koma (Commas)](#commas)
1. [Titik Koma (Semicolons)](#semicolons)
1. [Type Casting & Coercion](#type-casting--coercion)
1. [Penamaan](#naming-conventions)
1. [Accessors](#accessors)

## Tipe Data

<a name="types--primitives"></a><a name="1.1"></a>

- [1.1](#types--primitives) **Primitives**: Saat mengakses tipe data primitif, tipe data akan langsung terdefinisi berdasarkan nilainya (value).

  - `string`
  - `number`
  - `boolean`
  - `null`
  - `undefined`
  - `symbol`
  - `bigint`

  ```javascript
  const foo = 1;
  let bar = foo;
  bar = 9;
  console.log(foo, bar); // => 1, 9
  ```

  - `Symbols` dan `BigInts` tidak dapat di-polyfill dengan tepat, sehingga tidak dapat digunakan saat menargetkan browser/enviroment yang belum didukung.

  > polyfill adalah kode yang mengimplementasikan fitur pada browser web yang tidak mendukung fitur tersebut.

<a name="types--complex"></a><a name="1.2"></a>

- [1.2](#types--complex) **Complex**: Saat mengakses tipe data kompleks, mereferensi langsung ke nilainya (value).

  - `object`
  - `array`
  - `function`

  ```javascript
  const foo = [1, 2];
  const bar = foo;
  bar[0] = 9;
  console.log(foo[0], bar[0]); // => 9, 9
  ```

**[⬆ Kembali ke daftar isi](#daftar-isi)**

## References

<a name="references--prefer-const"></a><a name="2.1"></a>

- [2.1](#references--prefer-const) Gunakan `const` untuk semua reference dari sebuah variable yang dibuat; ganti penggunaan `var` dalam membuat sebuah variable. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

  > Kenapa? ini bertujuan untuk mengunci sebuah variable dari pengisian ulang(reassign) variable, karena bisa mengakibatkan bug yang lebih susah dideteksi dalam debugging.

  ```javascript
  // bad
  var a = 1;
  var b = 2;

  // good
  const a = 1;
  const b = 2;
  ```

<a name="references--disallow-var"></a><a name="2.2"></a>

- [2.2](#references--disallow-var) jika ingin mengisi ulang sebuah variable (reassign), pakai `let` ketimbang `var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

  > Kenapa? `let` adalah block-scoped variable ketimbang function-scoped seperti `var`.

  ```javascript
  // bad
  var count = 1;
  if (true) {
    count += 1;
  }

  // good, pakai let.
  let count = 1;
  if (true) {
    count += 1;
  }
  ```

<a name="references--block-scope"></a><a name="2.3"></a>

- [2.3](#references--block-scope) NB: `let` dan `const` itu block-scoped, dimana hanya `var` yang function-scoped.

  ```javascript
  // const dan let hanya muncul didalam blocks mereka tidak terdefinisi.
  {
    let a = 1;
    const b = 1;
    var c = 1;
  }
  console.log(a); // ReferenceError
  console.log(b); // ReferenceError
  console.log(c); // ter-Print 1
  ```

  didalam kode diatas, bisa dilihat `a` dan `b` akan me-return ReferenceError, tapi `c` akan menampilkan angka. ini karena `a` dan `b` itu block scoped, tapi `c` itu function-scoped.

  > bisa dicoba lewat terminal

**[⬆ Kembali ke daftar isi](#daftar-isi)**

## Objects

<a name="objects--no-new"></a><a name="3.1"></a>

- [3.1](#objects--no-new) gunakan syntax biasa (literal syntax) untuk membuat object baru. eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

  ```javascript
  // bad
  const item = new Object();
  // good
  const item = {};
  ```

<a name="es6-computed-properties"></a><a name="3.4"></a>

- [3.2](#es6-computed-properties) Pakai nama property saat membuat objects dengan nama properti yang dynamics.

  > Kenapa? dengan ini bisa mendifinisikan semua properti didalam satu tempat.

  ```javascript
  function getKey(k) {
    return `key dengan nama ${k}`;
  }

  // bad
  const obj = {
    id: 5,
    name: "Surabaya"
  };
  obj[getKey("enabled")] = true;

  // good
  const obj = {
    id: 5,
    name: "Surabaya",
    [getKey("enabled")]: true
  };
  ```

<a name="es6-object-shorthand"></a><a name="3.5"></a>

- [3.3](#es6-object-shorthand) Pakai shorthand saat membuat object method. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

  ```javascript
  // bad
  const atom = {
    value: 1,
    addValue: function (value) {
      return atom.value + value;
    }
  };

  // good
  const atom = {
    value: 1,
    addValue(value) {
      return atom.value + value;
    }
  };
  ```

<a name="es6-object-concise"></a><a name="3.6"></a>

- [3.4](#es6-object-concise) Pakai nama sebuah variable, jika properti memeiliki key yang sama dengan variable (property value shorthand). eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

  > Kenapa? lebih singkat dan descriptive.

  ```javascript
  const uzumakiNaruto = "Naruto Uzumaki";
  // bad
  const ninja = {
    uzumakiNaruto: uzumakiNaruto
  };

  // good
  const ninja = {
    uzumakiNaruto
  };
  ```

<a name="objects--grouped-shorthand"></a><a name="3.7"></a>

- [3.5](#objects--grouped-shorthand) Menempatkan shorthand dipaling atas dalam pembuatan object.

  > Kenapa? ini mempermudah dalam mendeteksi keberadaan shorthand.

  ```javascript
  const uzumakiNaruto = "Naruto Uzumaki";
  const sasukeUchiha = "Uchiha Sasuke";

  // bad
  const ninja = {
    madara: "Madara Uchiha",
    sasukeUchiha,
    hinata: "Hinata Hyuga",
    uzumakiNaruto
  };

  // good
  const ninja = {
    sasukeUchiha,
    uzumakiNaruto,
    madara: "Madara Uchiha",
    hinata: "Hinata Hyuga"
  };
  ```

<a name="objects--quoted-props"></a><a name="3.8"></a>

- [3.6](#objects--quoted-props) hanya quote / petik yang dipakai untuk mendifinisikan key yang tidak valid (invalid identifiers). eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

  > Kenapa? dalam kegiatan sehari" kita lebih mempertimbangkan kemudahan dalam membaca kode. dan bisa dideteksi IDE untuk meng highlight sebuah syntax, dan lebih mudah untuk engine js saat menjalankan script.

  ```javascript
  // bad
  const bad = {
    "foo": 3,
    "bar": 4,
    "data-blah": 5
  }; // sebenarnya valid, tetapi vscode / IDE lain susah untuk menebak key dari object

  // good
  const good = {
    foo: 3,
    bar: 4,
    "data-blah": 5
  };
  ```

<a name="objects--prototype-builtins"></a>

- [3.7](#objects--prototype-builtins) Jangan pernah memanggil `Object.prototype` methods secara langsung, seperti `hasOwnProperty`, `propertyIsEnumerable`, dan `isPrototypeOf`. eslint: [`no-prototype-builtins`](https://eslint.org/docs/rules/no-prototype-builtins)

  > Kenapa? sebuah methods mungkin dimiliki juga didalam properti pada objek yang dimaksud, `{ hasOwnProperty: false }` - atau, object kemungkinan `null` atau object kosong (`Object.create(null)`).

  ```javascript
  // bad
  console.log(object.hasOwnProperty(key));

  // good
  console.log(Object.prototype.hasOwnProperty.call(object, key));

  // best
  const has = Object.prototype.hasOwnProperty; // cache diawal, di module scope.
  console.log(has.call(object, key));

  /* atau menggunakan cara aman untuk mencari key dalam object */
  import has from "has"; // https://www.npmjs.com/package/has
  console.log(has(object, key));
  ```

<a name="objects--rest-spread"></a>

- [3.8](#objects--rest-spread) Prefer ke object spread syntax dari pada [`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) untuk shallow-copy / (copy full) sebuah objects. Gunakan object rest parameter syntax untuk membuat object baru dengan properti yang sama. eslint: [`prefer-object-spread`](https://eslint.org/docs/rules/prefer-object-spread)

  ```javascript
  // very bad
  const original = { a: 1, b: 2 };
  const copy = Object.assign(original, { c: 3 }); // ini merubah / mutates `original` ಠ_ಠ
  delete copy.a; // sama juga seperti ini

  // bad
  const original = { a: 1, b: 2 };
  const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

  // good
  const original = { a: 1, b: 2 };
  const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }
  const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
  ```

**[⬆ Kembali ke daftar isi](#daftar-isi)**
