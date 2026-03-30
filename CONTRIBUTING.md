# Contributing to Mint

> [!INFO]
>
> If you're reading this and you've just forked this repository, you may want to replace all mentions of the Mint toolchain with your extension's name.

## What You'll Need

1. Any semi-new version of Git
2. A GitHub account
3. Node.js and `npm` installed
4. Working knowledge of JavaScript, YAML, or JSON

## Understanding the Build Script

Mint's build script is something called a "bundler", which means it concatenates *(or combines)* a set of files into one. In Mint's case, the files it bundles are called "modules" or "ES modules". If you know about Webpack, you'll know exactly what we mean.

The build process outputs three files:

1. `build/extension.js`,
2. `build/min.extension.js` *(if you have `terser`)*, and
3. `build/pretty.extension.js` *(if you have `prettier`)*.

If you ran `npm ci` before building, you will have installed `prettier` and `terser` already. If not, `min.extension.js` and `pretty.extension.js` will not appear. No problem!

## Understanding TurboWarp extensions

> [!INFO]
>
> We have since removed this section to remove the overhead of updating this field if TurboWarp's extension system changes. **If you want guidance, see [TurboWarp's documentation](https://docs.turbowarp.org/development/extensions/introduction).**

## Triflare's Stance on Quality

### Using LLMs to Generate Extensions

If AI code is used, it should meet or exceed human standards. We have both humans *(Triflare's dedicated reviewer team)* and AIs *(CodeRabbit & GitHub Copilot)* review all Pull requests to ensure they meet this standard.

> [!WARNING]
>
> A recent U.S. case found that purely AI-generated code may not be eligible for U.S. copyright protection and can be treated as public domain. However, any portions that a human author created or that a human has substantially modified remain eligible for copyright and may be licensed by their copyright holders. This warning applies only to the purely machine-generated parts; human-authored or significantly edited contributions can be copyrighted and licensed.

## Quality Over All

Triflare believes in quality over quantity. We want to keep our tools opinionated, so we will keep ensuring quality to keep it that way. For example, our goal is to turn Mint into something that all TurboWarp extension developers use to code their extensions.
