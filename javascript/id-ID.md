# Javascript Clean Code Bahasa Indonesia


## Table of Contents

  1. [Tipe Data](#tipe-data)
  1. [Referensi](#references)
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

    - Symbols dan BigInts tidak dapat di-polyfill dengan tepat, sehingga tidak dapat digunakan saat menargetkan browser/enviroment yang belum didukung.
    
    > polyfill adalah kode yang mengimplementasikan fitur pada browser web yang tidak mendukung fitur tersebut.

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **Complex**: Saat mengakses tipe data kompleks, mereferensi langsung ke nilainya (value).

    - `object`
    - `array`
    - `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;
    bar[0] = 9;
    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ Kembali ke daftar isi](#table-of-contents)**