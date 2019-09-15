# math-input

A WebComponent form element for inputting mathematical expressions. Spiritual successor of [adm-math](https://github.com/wyattpeak/adm-math).

This component defines the `<math-input>` field, which behaves as a regular form element. Its `value` attribute contains a representation of the typed expression in [content MathML](https://www.w3.org/TR/MathML3/chapter4.html).

## Installation

The component is contained in two JavaScript files and one CSS file, `math-input.js`, `math-node.js` and `math-input.css`. Simply download them into your project folder, ensuring that the two JavaScript files are in the same directory.

## Testing (for development)

Testing is handled by Jest testing framework. To install the required dependencies, run `yarn install` in the project directory.

To execute the tests, run `yarn test`.

## Usage

First include the module and stylesheet:

```html
<link rel="stylesheet" href="math-input.css"></link>
<script type="module" src="math-input.js"></script>
```

**Note:** Due to the expanding nature of the input, if you wish to change its size use the `min-width` and `min-height` properties instead of `width` and `height`.

Then use it as a regular form element:

```html
<form...>
    <math-input name="fieldName" tabindex="1"></math-input>
</form>
```

**Note:** Due to WebComponent limitations, you must give the field a `tabindex`.

## Math Support

The field will accept the following characters as input:

`[a-zA-Z0-9α-ωΑ-Ω.+\-*\/()\|^]`

Most of the letters will be parsed as individual unknowns. Typing `xy`, for instance, will be interpreted as 'x times y'. There are, however, a few exceptions:

| Input | Interpretation |
| ----- | -------------- |
| `e`   | Euler's number ≈ 2.718 |
| `π`   | The constant π ≈ 3.142 |
| `pi`  | The constant π ≈ 3.142 |
| `sin` | The sine function |
| `cos` | The cosine function |
| `tan` | The tangent function |
| `ln`  | The natural log function |

### Input Buttons

The field will also accept the following elements, which can't be easily typed:

| Element     | Symbol  |
| ----------- | ------- |
| Square root | `sqrt`  |
| π           | `pi`    |
| ∞           | `infty` |

To input one of these, set the `<math-input>`'s `insert` attribute to its symbol in the right hand column. A buttton to add a square root symbol, for instance, might look like this:

```html
<input type="button" value="Square Root" onclick="document.getElementsByName('fieldName')[0].setAttribute('insert', 'sqrt');" />
```

Any value which could be inserted by keyboard can also be inserted in this way. A button for '0', for example, would look like this:

```html
<input type="button" value="0" onclick="document.getElementsByName('fieldName')[0].setAttribute('insert', '0');" />
```

The attribute will auto-clear when the element has been inserted, there's no need to clear it before inserting another element.