# Cumulative Layout Shift (CLS) Chrome Extension

![An example of a good 1s CLS score (thus green!)](cls-example-1s.png)

This Chrome extension tracks the [CLS (Cumulative Layout Shift)](https://web.dev/cls/ "web.dev article on CLS") metric for pages that you visit as you browse the Web.

## Installation

This is very alpha! I haven't put the extension in the store yet, so, clone the repo and then go to chrome://extensions. Once there, click on the "Load unpacked" button and select the directory that you just cloned.

## Features

- As CLS events are sent to the extension from the [PerformanceObserver](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver) the icon will update by changing color (green for good, yellow for adequate, and red for pood) and showing the number of seconds in the badge. If it takes longer than 9999 seconds, it will just say "BAD" because the badge can only show 4 characters and .... well it _is_ really bad
- Click on the icon UI to turn the extension on or off (it will show a red square if off, and a green one if there isn't an existing CLS score for on)
- It stores the CLS for the load in local storage, so when you go back it can show you the score from earlier

## Bugs / Issues

- It doesn't handle multiple windows well, so the icon UI may be showing the run from the last tab in the window
- If you don't see results from a page, it may be that the result hasn't come back, or it may be the item below..
- If you aren't seeing results on an internal site or see an error `"This page cannot be scripted due to an ExtensionsSettings policy."` it means that your organization is limiting content scripts (often on internal content). To fix this, you need to add a `key: $TOKEN_FROM_YOUR_ORGANIZATION` to the `manifest.json`

# Metrics

| Color  | Description |
| ------ | ----------- |
| GREEN  | good        |
| YELLOW | adequate    |
| RED    | poor        |

## CLS thresholds

| Color  | Threshold |
| ------ | --------- |
| GREEN  | < 0.1     |
| YELLOW | < 0.25    |
| RED    | > 0.25    |

## Other metrics as FYI:

```
LCP: GREEN < 2.5 second,       YELLOW < 4s,    RED > 4s
FCP: GREEN < 1s,               YELLOW < 3s,    RED > 300ms
FID: GREEN < 100 milliseconds, YELLOW < 300ms, RED > 300ms
```

# States

- Extension is on, but no results for this tab: "CLS" with a [green] square
- Extension is off, but no results for this tab: "CLS" with a [red] square
- CLS is good: Green background with score in badge
- CLS is adequate: Yellow background with score in badge
- CLS is poor: Red background with score in badge, or "BAD" if the score is greater than 9999 due to a badge only allowing 4 characters