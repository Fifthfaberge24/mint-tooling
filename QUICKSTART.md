# Get Up and Running

You can get your extension up in a few minutes!

> [!INFO]
>
> If `npm` reports vulnerabilities, please use GitHub's security reporting feature or send an e-mail to `triflare.dev@proton.me`. We aim to acknowledge reports within 72 hours and provide a full response within 90 days.

1. Run `npm ci`.

2. Run `npm run fullstack`.
3. Copy the file in `build/extension.js`.
4. Open TurboWarp and enter the custom extension import screen.
5. Choose "Text" *(or "File" if you have it downloaded)*, then paste `build/extension.js`'s content into the box below. Click "Run unsandboxed" and "Load".
6. You're done! If the extension does not add any blocks to your palette, check your console by pressing `ctrl + shift + i` and clicking "Console". If there are any errors after the string of random characters you'll see after importing the extension, contact the repository's developer *(us if you're running this from `triflare/mint-tooling`)*.

It's that simple!

# Build Your Extension

> [!INFO]
>
> We have since removed this section to remove the overhead of updating this field if TurboWarp's extension system changes. **If you want guidance, see [TurboWarp's documentation](https://docs.turbowarp.org/development/extensions/introduction).**
