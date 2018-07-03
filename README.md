# Cryptoformat

[![Build Status](https://img.shields.io/travis/coingecko/cryptoformat.svg?style=flat-square)](https://travis-ci.org/coingecko/cryptoformat)
[![NPM package](https://img.shields.io/npm/v/@coingecko/cryptoformat.svg?style=flat-square)](https://www.npmjs.com/package/coingecko/cryptoformat)
![NPM license](https://img.shields.io/npm/l/@coingecko/cryptoformat.svg?style=flat-square)

`cryptoformat` is used by coingecko.com to format crypto and fiat values.

Often an altcoin can be worth much less than $0.01 USD, and thus we need to format this value by providing more decimal places in the formatting to prevent losing precious information.

`cryptoformat` also tries to handle different locales and currency formatting by deferring the work to the browser's [`Intl.NumberFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat). If `Intl.NumberFormat` is not supported by the browser, `cryptoformat` provides a primitive fallback for currency display.

## Install

```
npm i @coingecko/cryptoformat
```

## Usage

```js
import { formatCurrency } from "@coingecko/cryptoformat";

formatCurrency(123, "USD", "en");
// "$123.00"

formatCurrency(0.00123, "USD", "en");
// "$0.00123000"

// Provide raw = true to remove formatting and symbol
formatCurrency(0.00123, "USD", "en", true);
// "0.00123000"

formatCurrency(123400, "IDR", "id");
// "Rp123.400"

formatCurrency(123400, "EUR", "de");
// "123.400 €"
```

## Known Issues

1.  `Intl.NumberFormat` does not always behave consistently across browsers. `cryptoformat` does some manual overrides in order to ensure that "MYR123.00" is displayed as "RM123.00", for example.
2.  Given that country detection for locale is quite hard to do, e.g. "en-MY", `cryptoformat` does not try to do country sniffing. It is the responsibility of the caller to provide that if possible, but providing only "en" should also work for the most part, but not perfectly: users in different regions may expect a different formatting for the same language.
