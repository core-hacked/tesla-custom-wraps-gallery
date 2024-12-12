# Tesla (Custom) Wraps Gallery | T(C)WG

## Introduction

This is a gallery of custom wraps for Tesla vehicles (currently limited to Cybertruck). The gallery is a community-driven project and is not monetized in any way. The gallery is intended as a place to share, preview and download custom wraps for Tesla vehicles.

## How to contribute

To contribute to the gallery, please follow the steps below:

1. Fork the repository
2. Create a new folder in the `/static/wraps` directory with your github handle
3. Add your wrap files to the folder you created
4. Add (or update) your data in the `index.json` file with the following format:

```json
[
  [...]
  {
    "author": "your-github-handle",
    "wraps": [
      {
        "name": "Your Wrap",
        "path": "your-wrap.png",
        "dont-crop": false,
      }
    ]
  }
]

```

You can also add a `dont-crop: true` property to the wrap object if you don't want the image to be cropped, in case you need to showcase the full wrap design.
More options may be added in the future.

5. Create a pull request

## How to download / install wraps

See [this guide](https://github.com/teslamotors/custom-wraps) from Tesla's official repository.

---

## Dependencies

1. Tailwind CSS
2. JSZip
3. TDS (Tesla Design System - Compiled CSS File, pulled from cdn-design.tesla.com | v9.1.2)
4. Cyber-Theme.css - Locally embedded

> Note: All assets or brand names are property of their respective owners, Cybertruck, Model S, Model 3, Model X, Model Y, Tesla, and the "Tesla" logo are trademarks of Tesla, Inc.

## License

All assets, excluding community contributions, belong to Tesla, Inc. and are protected by copyright, trademark, and other intellectual property laws. All rights not expressly granted to you are reserved by Tesla, Inc.

The code/project is licensed separately under the MIT license, excluding the Tesla assets.
For takedown requests, please contact the repository owner under: me@corehacked.com
