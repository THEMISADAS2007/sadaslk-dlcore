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
import { ytmp3, youtube, facebook, tiktok, instagram, twitter } from 'sadaslk-dlcore';

const run = async () => {
  const y = await ytmp3('https://youtu.be/VIDEO_ID', { bitrate: '192kbps' });
  console.log('YouTube MP3:', y.audio.url);

  const fb = await facebook('https://www.facebook.com/watch/?v=VIDEO_ID');
  console.log('Facebook best:', fb.best.url);
};

run();
```

```js
// CommonJS
const { ytmp3, youtube, facebook, tiktok, instagram, twitter } = require('sadaslk-dlcore');
```

---

## API

All functions return a **Promise** that resolves to a [Unified Result](#unified-result-shape).

### YouTube MP3

```ts
async function ytmp3(url: string, options?: {
  bitrate?: '128kbps' | '160kbps' | '192kbps' | '256kbps' | '320kbps';
  preferM4A?: boolean; // default false
  timeoutMs?: number;  // default 30000
}): Promise<UnifiedResult>
```

**Example**

```js
const res = await ytmp3('https://youtu.be/VIDEO_ID', { bitrate: '320kbps' });
console.log(res.audio); // { url, size, ext, bitrate }
```

### Facebook

```ts
async function facebook(url: string, options?: CoreOptions): Promise<UnifiedResult>
```

**Example**

```js
const res = await facebook('https://www.facebook.com/username/videos/123456/');
console.log(res.best.url);
```

### TikTok

```ts
async function tiktok(url: string, options?: { noWatermark?: boolean } & CoreOptions): Promise<UnifiedResult>
```

**Example**

```js
const res = await tiktok('https://www.tiktok.com/@user/video/123');
console.log(res.best.url);
```

### Instagram

```ts
async function instagram(url: string, options?: CoreOptions): Promise<UnifiedResult>
```

**Example**

```js
const res = await instagram('https://www.instagram.com/reel/ABC123/');
for (const f of res.formats) console.log(f.quality, f.url);
```

### X (Twitter)

```ts
async function twitter(url: string, options?: CoreOptions): Promise<UnifiedResult>
```

**Example**

```js
const res = await twitter('https://x.com/user/status/123456789');
console.log(res.best); // highest quality format
```

---

## Unified Result Shape

```ts
export type MediaFormat = {
  itag?: string | number;    // when available
  quality?: string;          // e.g. '720p', '1080p', 'hq', 'music-320kbps'
  mime?: string;             // 'video/mp4', 'audio/mpeg', ...
  size?: number | null;      // bytes, if known
  url: string;               // direct file url
  audioBitrate?: number;     // kbps
  videoFps?: number;         // fps
  ext?: string;              // mp4, m4a, mp3, webm, ...
}

export type UnifiedResult = {
  provider: 'youtube' | 'facebook' | 'tiktok' | 'instagram' | 'twitter';
  id?: string;
  url: string;               // original source url
  title?: string;
  author?: string;
  duration?: number | null;  // seconds
```
