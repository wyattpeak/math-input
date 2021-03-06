# math-input

A WebComponent form element for inputting mathematical expressions. Spiritual successor of [adm-math](https://github.com/wyattpeak/adm-math).

This component defines the `<math-input>` field, which behaves as a regular form element. Its `value` attribute contains a representation of the typed expression in [content MathML](https://www.w3.org/TR/MathML3/chapter4.html).

## Installation

The component is contained in two JavaScript files and one CSS file, `math-input.js`, `math-node.js` and `math-input.css`. Simply download them into your project folder, ensuring that the two JavaScript files are in the same directory.

## Testing (for development)

Testing is handled by Jest testing framework. To install the required dependencies, run `npm install` in the project directory.

To execute the tests, run `npm run test`.

## Usage

First, install the NPM dependencies (the only dependency is a polyfill to allow WebComponent support in old browsers and Edge). In the project directory, run:

```bash
$ npm install --production
```

In the HTML file, include the polyfill, module and stylesheet:

```html
<script src="node_modules/@webcomponents/webcomponentsjs/webcomponents-bundle.js"></script>

<link rel="stylesheet" href="math-input.css"></link>
<script type="module" src="math-input.js"></script>
```

**Note:** Due to the expanding nature of the `<math-input>` field, if you wish to change its size use the `min-width` and `min-height` properties instead of `width` and `height`.

Then use it as a regular form element:

```html
<form...>
    <math-input name="fieldname" tabindex="1"></math-input>
</form>
```

**Note:** Due to WebComponent limitations, you must give the field a `tabindex`.

The `value` attribute of the field will be a representation, in MathML, of whatever is typed in the field. If you type in `1+x`, the `value` attribute will contain:

```xml
<apply><plus /><cn>1</cn><ci>x</ci></apply>
```

The value of the field can also be preset by setting the `value` attribute, this will create a field with a value of 1 already entered:

```html
<form...>
    <math-input name="fieldname" tabindex="1" value="<cn>1</cn>"></math-input>
</form>
```

**Note:** The field's value cannot be changed after initialisation using the `value` attribute.

Refer to `examples/form.html` to see a full implementation.

## Math Support

The field will accept the following characters as input:

`[a-zA-Z0-9α-ωΑ-Ω.+\-*∞!\/()\|^]`

Most of the letters will be parsed as individual unknowns. Typing `xy`, for instance, will be interpreted as 'x times y'. There are, however, a few exceptions:

| Input | Interpretation |
| ----- | -------------- |
| `e`   | Euler's number ≈ 2.718 |
| `π`   | The constant π ≈ 3.142 |
| `pi`  | The constant π ≈ 3.142 |
| `sin` | The sine function |
| `cos` | The cosine function |
| `tan` | The tangent function |
| `arcsin` | The arcsine function |
| `arccos` | The arccosine function |
| `arctan` | The arctangent function |
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
<input type="button" value="Square Root" onclick="document.getElementById('fieldId').setAttribute('insert', 'sqrt');" />
```

**Note:** Be careful using document.getElementsByName() as the `<math-input>` field, on instantiation, will create a hidden input field with the same name to allow proper integration with forms.

Any value which could be inserted by keyboard can also be inserted in this way. A button for '0', for example, would look like this:

```html
<input type="button" value="0" onclick="document.getElementById('fieldId').setAttribute('insert', '0');" />
```

The attribute will auto-clear when the element has been inserted, there's no need to clear it before inserting another element.

### Other Actions

You can perform other actions by setting the field's `action` attribute. The current supported actions are:

| Action      | Description |
| ----------- | ----------- |
| `backspace` | Delete the symbol immediately left of the cursor |

A button which performed the backspace action would look like this:

```html
<input type="button" value="0" onclick="document.getElementById('fieldId').setAttribute('action', 'backspace');" />
```

The attribute will auto-clear when the action has been performed, there's no need to clear it before performing another action.
