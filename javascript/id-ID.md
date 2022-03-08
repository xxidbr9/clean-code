# Javascript Clean Code Bahasa Indonesia

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
  // good, use the let.
  let count = 1;
  if (true) {
    count += 1;
  }
  ```

<a name="references--block-scope"></a><a name="2.3"></a>

- [2.3](#references--block-scope) NB: `let` dan `const` itu block-scoped, dimana hanya `var` yang function-scoped.

  ```javascript
  // const and let only exist in the blocks they are defined in.
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
