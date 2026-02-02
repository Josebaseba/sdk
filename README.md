<div align="center">
  <img src="https://github.com/microlinkhq/cdn/raw/master/dist/banner/sdk.png#gh-light-mode-only" alt="microlink sdk">
  <img src="https://github.com/microlinkhq/cdn/raw/master/dist/banner/sdk-dark.png#gh-dark-mode-only" alt="microlink sdk">
  <br><br>
</div>

<div align="center">
  <a href="https://microlink.io"><img src="https://img.shields.io/badge/powered_by-microlink.io-blue?style=flat-square&color=%23EA407B" alt="Powered by microlink.io"></a>
  <a href="https://microlink.io/sdk"><img src="https://img.shields.io/badge/documentation-📚-blue?style=flat-square" alt="Documentation"></a>
  <a href="https://sdk-react.microlink.io"><img src="https://img.shields.io/badge/storybook-📖-green?style=flat-square" alt="Storybook"></a>
  <a href="https://sdk-vanilla.microlink.io/"><img src="https://img.shields.io/badge/vainilla demo-🍦-red?style=flat-square" alt="NPM Status"></a>
  <br><br>
</div>

> Turn links into beautiful previews

## Features

- **Rich Media Support** - Images, videos, audio, screenshots, and embedded iframes
- **Multiple Sizes** - Normal, small, and large card layouts
- **Lazy Loading** - IntersectionObserver-based with configurable threshold
- **Media Controls** - Full playback controls for video/audio with keyboard shortcuts
- **Theming** - CSS variables and contrast mode for automatic color adaptation
- **RTL Support** - Right-to-left text direction support
- **Hover Previews** - Show link previews on hover (separate packages)
- **Framework Agnostic** - React component and vanilla JS versions available

## Packages

| Package | Description | Version |
|---------|-------------|---------|
| [@microlink/react](https://www.npmjs.com/package/@microlink/react) | React component | ![npm](https://img.shields.io/npm/v/@microlink/react) |
| [@microlink/vanilla](https://www.npmjs.com/package/@microlink/vanilla) | Vanilla JavaScript | ![npm](https://img.shields.io/npm/v/@microlink/vanilla) |
| [@microlink/hover-react](https://www.npmjs.com/package/@microlink/hover-react) | React hover preview | ![npm](https://img.shields.io/npm/v/@microlink/hover-react) |
| [@microlink/hover-vanilla](https://www.npmjs.com/package/@microlink/hover-vanilla) | Vanilla hover preview | ![npm](https://img.shields.io/npm/v/@microlink/hover-vanilla) |

## Installation

### React

```bash
npm install @microlink/react styled-components --save
```

### Vanilla

```bash
npm install @microlink/vanilla --save
```

Or use the CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/@microlink/vanilla@latest/dist/microlink.min.js"></script>
```

### Hover Packages

```bash
# React
npm install @microlink/hover-react styled-components --save

# Vanilla
npm install @microlink/hover-vanilla --save
```

## Quick Start

### React

```jsx
import Microlink from '@microlink/react'

export default function App() {
  return <Microlink url="https://github.com" />
}
```

### Vanilla

```html
<a href="https://github.com">GitHub</a>

<script>
  microlink('a')
</script>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `url` | `string` | **required** | The URL to preview |
| `apiKey` | `string` | `undefined` | API key for authenticated requests |
| `size` | `'normal'` \| `'small'` \| `'large'` | `'normal'` | Card size |
| `media` | `string` \| `string[]` | `['iframe', 'video', 'audio', 'image', 'logo']` | Media type priority |
| `direction` | `'ltr'` \| `'rtl'` | `'ltr'` | Text direction |
| `contrast` | `boolean` \| `string` | `false` | Auto-adapt colors from image palette |
| `lazy` | `boolean` \| `object` | `true` | Enable lazy loading |
| `loading` | `boolean` | `undefined` | Manually control loading state |
| `fetchData` | `boolean` | `true` | Enable/disable API fetching |
| `setData` | `object` \| `function` | `undefined` | Override or customize data |
| `prerender` | `'auto'` \| `true` \| `false` | `'auto'` | Enable prerendering for SPAs |

### Media Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `autoPlay` | `boolean` | `true` | Auto-play video/audio |
| `controls` | `boolean` | `true` | Show playback controls |
| `loop` | `boolean` | `true` | Loop video/audio |
| `muted` | `boolean` | `true` | Mute video/audio |
| `playsInline` | `boolean` | `true` | Play video inline on mobile |
| `mediaRef` | `ref` \| `function` | `undefined` | Ref to the media element |

## Examples

### Card Sizes

```jsx
<Microlink url="https://github.com" size="small" />
<Microlink url="https://github.com" size="normal" />
<Microlink url="https://github.com" size="large" />
```

### Media Types

```jsx
// Show image (default)
<Microlink url="https://example.com" media="image" />

// Show logo
<Microlink url="https://example.com" media="logo" />

// Show video
<Microlink url="https://youtube.com/watch?v=..." media="video" />

// Show audio
<Microlink url="https://spotify.com/track/..." media="audio" />

// Show screenshot
<Microlink url="https://example.com" media="screenshot" />

// Embedded iframe (for supported providers)
<Microlink url="https://twitter.com/..." media="iframe" />

// Priority order (first available wins)
<Microlink url="https://example.com" media={['video', 'image', 'logo']} />
```

### Contrast Mode

Automatically adapts the card's colors based on the image's palette:

```jsx
<Microlink url="https://github.com" contrast />
```

### RTL Direction

```jsx
<Microlink url="https://github.com" direction="rtl" />
```

### Lazy Loading

```jsx
// Enabled by default
<Microlink url="https://github.com" lazy />

// With custom threshold
<Microlink url="https://github.com" lazy={{ threshold: 0.5 }} />

// Disable lazy loading
<Microlink url="https://github.com" lazy={false} />
```

### Custom Data

Override fetched data with an object:

```jsx
<Microlink
  url="https://example.com"
  setData={{
    title: 'Custom Title',
    description: 'Custom description',
    image: { url: 'https://example.com/image.jpg' }
  }}
/>
```

Or use a function to transform the data:

```jsx
<Microlink
  url="https://example.com"
  setData={(data) => ({
    ...data,
    title: data.title.toUpperCase()
  })}
/>
```

### Static Mode (No API Fetch)

```jsx
<Microlink
  url="https://example.com"
  fetchData={false}
  setData={{
    title: 'My Title',
    description: 'My Description',
    image: { url: 'https://example.com/image.jpg' }
  }}
/>
```

### Video/Audio Controls

```jsx
<Microlink
  url="https://youtube.com/watch?v=..."
  media="video"
  autoPlay={false}
  controls={true}
  loop={false}
  muted={false}
/>
```

### Media Element Reference

```jsx
<Microlink
  url="https://youtube.com/watch?v=..."
  media="video"
  mediaRef={(node) => {
    if (node) {
      console.log('Media element:', node)
    }
  }}
/>
```

## Keyboard Shortcuts

When media controls are enabled:

| Key | Action |
|-----|--------|
| `Space` | Play/Pause |
| `←` Left Arrow | Rewind 5 seconds |
| `→` Right Arrow | Forward 5 seconds |
| `M` | Toggle mute |

## CSS Customization

### CSS Variables

```css
.microlink_card {
  --microlink-max-width: 500px;
  --microlink-background-color: #fff;
  --microlink-hover-background-color: #f5f8fa;
  --microlink-border-width: 1px;
  --microlink-border-style: solid;
  --microlink-border-color: #e1e8ed;
  --microlink-hover-border-color: #8899a680;
  --microlink-color: #181919;
}
```

### CSS Class Names

| Class | Description |
|-------|-------------|
| `.microlink_card` | Main card container |
| `.microlink_card__content` | Content section |
| `.microlink_card__content_title` | Title element |
| `.microlink_card__content_description` | Description element |
| `.microlink_card__content_url` | URL footer |
| `.microlink_card__media` | Media section |
| `.microlink_card__media_image` | Image element |
| `.microlink_card__media_video` | Video element |
| `.microlink_card__media_audio` | Audio element |
| `.microlink_card__media__controls` | Media controls wrapper |
| `.microlink_card__iframe` | Iframe container |

### Custom Styles

```jsx
<Microlink
  url="https://github.com"
  style={{
    fontFamily: 'Helvetica, sans-serif',
    borderRadius: '8px',
    boxShadow: '0 1px 4px rgba(0, 0, 0, 0.2)'
  }}
/>
```

## Hover Previews

### React

```jsx
import MicrolinkHover from '@microlink/hover-react'

const Link = (props) => <a {...props} />

const HoverLink = MicrolinkHover(Link)

export default function App() {
  return (
    <HoverLink href="https://github.com">
      Hover over me!
    </HoverLink>
  )
}
```

### Vanilla

```html
<a href="https://github.com">GitHub</a>

<script src="https://cdn.jsdelivr.net/npm/@microlink/hover-vanilla@latest/dist/microlink.min.js"></script>
<script>
  microlink('a')
</script>
```

## Exported Utilities

The React package exports additional utilities:

```js
import Microlink, { imageProxy, getApiUrl, fetchFromApi } from '@microlink/react'

// Proxy images through microlink's image service
const proxiedUrl = imageProxy('https://example.com/image.jpg')

// Generate API URL with options
const [apiUrl, apiUrlProps] = getApiUrl({
  url: 'https://github.com',
  media: ['image'],
  // ... other options
})

// Fetch data from API
const { data } = await fetchFromApi(apiUrl, apiUrlProps)
```

## Vanilla Usage

### Query Selector

```js
// Single selector
microlink('.link')

// Multiple elements
microlink('a.preview-link')

// DOM element
microlink(document.querySelector('#my-link'))
```

### Data Attributes

```html
<a href="https://github.com"
   data-media="video"
   data-size="large"
   data-contrast="true"
   data-set-data='{"title": "Custom Title"}'>
  GitHub
</a>
```

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Peer Dependencies

### React Package
- `react` >= 17
- `react-dom` >= 17
- `styled-components` >= 5

## Related

- [microlink.io](https://microlink.io) - Microlink API
- [@microlink/mql](https://github.com/microlinkhq/mql) - Microlink Query Language

## License

**microlink** © [Microlink](https://microlink.io), Released under the [MIT](https://github.com/microlinkhq/sdk/blob/master/LICENSE.md) License.<br>
Authored and maintained by [Kiko Beats](https://kikobeats.com) with help from [contributors](https://github.com/microlinkhq/sdk/contributors).

> [microlink.io](https://microlink.io) · GitHub [@MicrolinkHQ](https://github.com/microlinkhq) · X [@microlinkhq](https://x.com/microlinkhq)
