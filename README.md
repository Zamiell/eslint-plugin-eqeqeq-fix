# eslint-plugin-eqeqeq-fix

## What is this?

This is a replacement for the ESLint [eqeqeq rule](https://eslint.org/docs/rules/eqeqeq) that allows automatic fixing.

<br />

### How do I use it?

* `npm install --save-dev eslint-plugin-eqeqeq-fix`
* Add  `plugin-eqeqeq-fix` to the `plugins` section of your `.eslintrc.js` file:
* Add the `eqeqeq-fix/eqeqeq` rule.
* Turn off the normal `eqeqeq` rule, if you have it enabled, so that they don't overlap. (For example, the `eqeqeq` rule is included in the [Airbnb config](https://github.com/airbnb/javascript) and a lot of other standard ESLint configs.)

For reference, this is a `.eslintrc.js` file that only enables this rule and nothing else:

```js
module.exports = {
  "plugins": ["eqeqeq-fix"],
  "rules": {
    "eqeqeq-fix/eqeqeq": "warn",
  },
};
```

<br />

## Why should I use this?

The ESLint [eqeqeq rule](https://eslint.org/docs/rules/eqeqeq) will throw an error if you use `==`, complaining that you should convert it to `===`. This is a fantastic rule, as the use of `==` is almost always a bug.

However, the eqeqeq rule will not automatically fix this for you when using the `--fix` flag, like most other ESLint rules do. This is [intentional](https://github.com/eslint/eslint/issues/4578) because doing so would break code was designed to use [loose equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#loose_equality_using). In general, the --fix flag is only meant to change the formatting of code, not the actual execution nature of the code.

With that said, in most modern code, intentional use of the `==` is operator is rare because it results in code that is hard to read and less explicit. Thus, most modern ESLint users will never have to worry about this potential code-breakage.

If you know for sure that your code base does not use any instances of `==`, then use this plugin to make this rule automatically `--fix`able. Doing so will allow you to type one less equals keystroke for every single if statement that you write! (Assuming that you use `eslint --fix` on-save, like many people do nowadays.)

<br />

### How did you make this?

* I copied [the ESLint source code](https://github.com/eslint/eslint/blob/master/lib/rules/eqeqeq.js) into a new rule plugin.
* I didn't have to do anything else - for some reason, `--fix` just automatically works.

<br />
