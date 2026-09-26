<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# sgemm

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Perform the matrix-matrix operation `C = α*op(A)*op(B) + β*C` where `op(X)` is one of the `op(X) = X`, or `op(X) = X^T`.

<section class="installation">

## Installation

```bash
npm install @stdlib/blas-base-sgemm
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var sgemm = require( '@stdlib/blas-base-sgemm' );
```

#### sgemm( ord, ta, tb, M, N, K, α, A, lda, B, ldb, β, C, ldc )

Performs the matrix-matrix operation `C = α*op(A)*op(B) + β*C` where `op(X)` is either `op(X) = X` or `op(X) = X^T`, `α` and `β` are scalars, `A`, `B`, and `C` are matrices, with `op(A)` an `M` by `K` matrix, `op(B)` a `K` by `N` matrix, and `C` an `M` by `N` matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 4.0 ] );
var B = new Float32Array( [ 1.0, 1.0, 0.0, 1.0 ] );
var C = new Float32Array( [ 1.0, 2.0, 3.0, 4.0 ] );

sgemm( 'row-major', 'no-transpose', 'no-transpose', 2, 2, 2, 1.0, A, 2, B, 2, 1.0, C, 2 );
// C => <Float32Array>[ 2.0, 5.0, 6.0, 11.0 ]
```

The function has the following parameters:

-   **ord**: storage layout.
-   **ta**: specifies whether `A` should be transposed, conjugate-transposed, or not transposed.
-   **tb**: specifies whether `B` should be transposed, conjugate-transposed, or not transposed.
-   **M**: number of rows in the matrix `op(A)` and in the matrix `C`.
-   **N**: number of columns in the matrix `op(B)` and in the matrix `C`.
-   **K**: number of columns in the matrix `op(A)` and number of rows in the matrix `op(B)`.
-   **α**: scalar constant.
-   **A**: first input matrix stored in linear memory as a [`Float32Array`][mdn-float32array].
-   **lda**: stride of the first dimension of `A` (leading dimension of `A`).
-   **B**: second input matrix stored in linear memory as a [`Float32Array`][mdn-float32array].
-   **ldb**: stride of the first dimension of `B` (leading dimension of `B`).
-   **β**: scalar constant.
-   **C**: third input matrix stored in linear memory as a [`Float32Array`][mdn-float32array].
-   **ldc**: stride of the first dimension of `C` (leading dimension of `C`).

The stride parameters determine how elements in the input arrays are accessed at runtime. For example, to perform matrix multiplication of two subarrays

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 0.0, 0.0, 3.0, 4.0, 0.0, 0.0 ] );
var B = new Float32Array( [ 1.0, 1.0, 0.0, 0.0, 0.0, 1.0, 0.0, 0.0 ] );
var C = new Float32Array( [ 1.0, 2.0, 3.0, 4.0 ] );

sgemm( 'row-major', 'no-transpose', 'no-transpose', 2, 2, 2, 1.0, A, 4, B, 4, 1.0, C, 2 );
// C => <Float32Array>[ 2.0, 5.0, 6.0, 11.0 ]
```

<!-- lint disable maximum-heading-length -->

#### sgemm.ndarray( ta, tb, M, N, K, α, A, sa1, sa2, oa, B, sb1, sb2, ob, β, C, sc1, sc2, oc )

Performs the matrix-matrix operation `C = α*op(A)*op(B) + β*C`, using alternative indexing semantics and where `op(X)` is either `op(X) = X` or `op(X) = X^T`, `α` and `β` are scalars, `A`, `B`, and `C` are matrices, with `op(A)` an `M` by `K` matrix, `op(B)` a `K` by `N` matrix, and `C` an `M` by `N` matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 4.0 ] );
var B = new Float32Array( [ 1.0, 1.0, 0.0, 1.0 ] );
var C = new Float32Array( [ 1.0, 2.0, 3.0, 4.0 ] );

sgemm.ndarray( 'no-transpose', 'no-transpose', 2, 2, 2, 1.0, A, 2, 1, 0, B, 2, 1, 0, 1.0, C, 2, 1, 0 );
// C => <Float32Array>[ 2.0, 5.0, 6.0, 11.0 ]
```

The function has the following additional parameters:

-   **sa1**: stride of the first dimension of `A`.
-   **sa2**: stride of the second dimension of `A`.
-   **oa**: starting index for `A`.
-   **sb1**: stride of the first dimension of `B`.
-   **sb2**: stride of the second dimension of `B`.
-   **ob**: starting index for `B`.
-   **sc1**: stride of the first dimension of `C`.
-   **sc2**: stride of the second dimension of `C`.
-   **oc**: starting index for `C`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameters support indexing semantics based on starting indices. For example,

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 0.0, 0.0, 1.0, 3.0, 2.0, 4.0 ] );
var B = new Float32Array( [ 0.0, 1.0, 0.0, 1.0, 1.0 ] );
var C = new Float32Array( [ 0.0, 0.0, 0.0, 1.0, 3.0, 2.0, 4.0 ] );

sgemm.ndarray( 'no-transpose', 'no-transpose', 2, 2, 2, 1.0, A, 1, 2, 2, B, 1, 2, 1, 1.0, C, 1, 2, 3 );
// C => <Float32Array>[ 0.0, 0.0, 0.0, 2.0, 6.0, 5.0, 11.0 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `sgemm()` corresponds to the [BLAS][blas] level 3 function [`sgemm`][blas-sgemm].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-array-discrete-uniform' );
var sgemm = require( '@stdlib/blas-base-sgemm' );

var opts = {
    'dtype': 'float32'
};

var M = 3;
var N = 4;
var K = 2;

var A = discreteUniform( M*K, 0, 10, opts ); // 3x2
var B = discreteUniform( K*N, 0, 10, opts ); // 2x4
var C = discreteUniform( M*N, 0, 10, opts ); // 3x4

sgemm( 'row-major', 'no-transpose', 'no-transpose', M, N, K, 1.0, A, K, B, N, 1.0, C, N );
console.log( C );

sgemm.ndarray( 'no-transpose', 'no-transpose', M, N, K, 1.0, A, K, 1, 0, B, N, 1, 0, 1.0, C, N, 1, 0 );
console.log( C );
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/blas/base/sgemm.h"
```

#### TODO

TODO.

```c
TODO
```

TODO

```c
TODO
```

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

### Examples

```c
TODO
```

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-base-sgemm.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-base-sgemm

[test-image]: https://github.com/stdlib-js/blas-base-sgemm/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-base-sgemm/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-base-sgemm/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-base-sgemm?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-base-sgemm.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-base-sgemm/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-base-sgemm/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-base-sgemm/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-base-sgemm/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-base-sgemm/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-base-sgemm/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-base-sgemm/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-base-sgemm/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-base-sgemm/main/LICENSE

[blas]: http://www.netlib.org/blas

[blas-sgemm]: https://www.netlib.org/lapack/explore-html/dd/d09/group__gemm_ga8cad871c590600454d22564eff4fed6b.html#ga8cad871c590600454d22564eff4fed6b

[mdn-float32array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

</section>

<!-- /.links -->
