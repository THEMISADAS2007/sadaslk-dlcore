# sadaslk-dlcore

> Simple, fast media extractor for YouTube (MP3/MP4), Facebook, TikTok, Instagram, and X (Twitter).
> Built for Node.js with clean, consistent results.

<p align="center">
  <a href="#installation"><img alt="npm" src="https://img.shields.io/badge/npm-sadaslk--dlcore-red"></a>
  <a href="#api"><img alt="api" src="https://img.shields.io/badge/API-stable-blue"></a>
  <a href="#license"><img alt="license" src="https://img.shields.io/badge/license-MIT-green"></a>
</p>

---

## Table of Contents

* [Features](#features)
* [Installation](#installation)
* [Quick Start](#quick-start)
* [API](#api)

  * [YouTube MP3](#youtube-mp3)
  * [Facebook](#facebook)
  * [TikTok](#tiktok)
  * [Instagram](#instagram)
  * [X (Twitter)](#x-twitter)
* [Unified Result Shape](#unified-result-shape)
* [Options](#options)
* [TypeScript](#typescript)
* [Error Handling](#error-handling)
* [Rate Limits & Proxies](#rate-limits--proxies)
* [Examples](#examples)
* [FAQ](#faq)
* [License](#license)
* [Disclaimer](#disclaimer)

---

## Features

* ✅ **YouTube MP3/MP4**: quick audio extraction with selectable bitrate/format
* ✅ **Facebook**: public video download (reels, posts)
* ✅ **TikTok**: with/without watermark
* ✅ **Instagram**: posts, reels, carousel (image/video)
* ✅ **X (Twitter)**: video and GIF
* ✅ **Uniform output** across all providers (title, duration, thumb, formats)
* ✅ **Zero native deps** — pure Node.js
* ✅ **ESM & CommonJS** support

> **Note:** Private/age-restricted/region-locked content may require cookies (see [Rate Limits & Proxies](#rate-limits--proxies)).

---

## Installation

```bash
npm i sadaslk-dlcore
# or
yarn add sadaslk-dlcore
# or
pnpm add sadaslk-dlcore
```

Node.js 18+ recommended.

---

## Quick Start

```js
// ESM
const { ytmp3, tiktok, facebook, instagram, twitter, ytmp4 } = require('sadaslk-dlcore');

(async () => {
  const mp3 = await ytmp3("youtube url");
  console.log(mp3);
})();

(async () => {
const mp4dl = await ytmp4("youtube url", {
      format: "mp4",
      videoQuality: "720"
    });
console.log("mp4dl);
})();

(async () => {
  const fb = await facebook("facebook url");
  console.log(mp3);
})();

(async () => {
  const tt = await tiktok("tiktok url");
  console.log(tt);
})();

(async () => {
  const ig = await instagram("instagram url");
  console.log(ig);
})();

(async () => {
  const tw = await twitter("twitter url");
  console.log(tw);
})();

```


