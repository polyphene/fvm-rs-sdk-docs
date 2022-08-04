# FVM Rust SDK Docs

[![Project icon.](https://img.shields.io/badge/project-IPFS-blue.svg?style=flat-square)](http://ipfs.io/)

This repository contains the documentation for the FVM Rust SDK. If you'd just like to read the Lotus docs, head to https://polyphene.github.io/fvm-rs-sdk-docs/.

## Get involved

We would **love ❤️ your help** to improve existing items or make new ones even better!

### Issues

If you find something wrong within this repository, please raise an [issue here →](https://github.com/polyphene/fvm-rs-sdk-docs/issues).

If you are attempting to close an issue, great! Thanks for the help! Please leave a comment within the issue requesting to be assigned to that issue **before** submitting a pull request. This minimizes the chance of multiple different contributors duplicating work by submitting pull requests for the same issue. If you submit a pull request to an issue _without_ first being assigned to it, that pull request may not be accepted.

### Suggestions

Everyone has an opinion when it comes to docs, and **that's a good thing**! Having folks from different backgrounds add to a discussion empowers everyone within that discussion. So if you've got something to add or would like to bring up a topic for discussion about the FVM Rust SDK, please do so!

#### Pull requests welcome

Feel free to submit pull requests with any changes you'd like to see!

## Project set up

If you want to build this site locally, run the following:

1. Clone this repository:

   ```bash
   git clone https://github.com/polyphene/fvm-rs-sdk-docs.git
   ```

1. Move into the `fvm-rs-sdk-docs` folder and install the NPM dependencies:

   ```bash
   cd fvm-rs-sdk-docs
   npm install
   ```

1. Boot up the application in _dev mode_:

   ```bash
   npm start
   ```

1. Open [localhost:1313](http://localhost:1313/) in your browser.
1. Close the local server with `CTRL` + `c`.
1. To restart the local server, run `npm start` from within the `fvm-rs-sdk-docs` folder.
1. To publish the site run: ```npm run build``` The project will be built and saved to /public.

