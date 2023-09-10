# Base64-to-Tensor

This package enables the conversion of Base64-encoded images to tensor objects using pure JavaScript, compatible with TensorFlow.js.

## Installation

Install the package using npm:

```bash
npm install base64-to-tensor --save
```

## Prerequisites

Ensure `@tensorflow/tfjs-core` is installed alongside a valid TensorFlow backend. Choose between the synchronous package [jpeg-js](https://github.com/jpeg-js/jpeg-js) for full blocking sync or the asynchronous package [sharp](https://github.com/lovell/sharp) for non-blocking async operations:

```sh
# For synchronous operations:
npm install @tensorflow/tfjs-core jpeg-js

# For asynchronous operations:
npm install @tensorflow/tfjs-core sharp
```

## Usage

Refer to the [convert.test.ts](./__tests__/convert.test.ts) file for example usage. Below are snippets demonstrating both synchronous and asynchronous conversions:

```typescript
import { convert, convertAsync } from "base64-to-tensor";
import { setBackend } from "@tensorflow/tfjs-core";
import "@tensorflow/tfjs-backend-wasm";

await setBackend("wasm");

// Synchronous conversion (jpeg-js)
const tensorSync = convert(mybase64); // Ensure mybase64 is a valid JPEG

// Asynchronous conversion (sharp)
const tensorAsync = await convertAsync(mybase64); // Enhanced performance

// Example tensor output
{
  kept: false,
  isDisposedInternal: false,
  shape: [189, 300, 3],
  dtype: "int32",
  size: 170100,
  strides: [900, 3],
  dataId: { id: 1 },
  id: 1,
  rankType: "3",
}
```

## Benefits

Using pure JavaScript for image conversion to tensors offers several advantages:

1. **Reduced Size and Portability**: Eliminates the need for `cairo` or other native image development converters.
2. **Increased Speed**: Performs calculations on-the-fly without external call overheads.
3. **Worker Thread Compatibility**: Facilitates the use of TensorFlow WASM backends within API services, enhancing performance and scalability.

## Benchmarks

<h3>Performance Benchmarks</h3>
<p>Performance benchmarks conducted on a Mac M1 (64GB RAM):</p>
<table>
  <thead>
    <tr>
      <th>Test Case</th>
      <th>Characters</th>
      <th>Size</th>
      <th>Synchronous</th>
      <th>Asynchronous</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>JPEG</td>
      <td>26,791</td>
      <td>26.16 KB</td>
      <td>100 ms</td>
      <td>50 ms</td>
    </tr>
  </tbody>
</table>
