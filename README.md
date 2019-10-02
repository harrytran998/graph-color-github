# graph-color-github

Change color in Graph contributions &amp; Contribution activity

## Result

![Imge](https://i.imgur.com/EibiF24.png)

## Guide

1. Install [Tamplemonkey extension](Link: https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en)

2. Clicks on "Create new Script"

3. Copy & Paste code

```js
// ==UserScript==
// @name         Graph Color Github
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        https://github.com/*
// @grant        none
// ==/UserScript==

/*
 * You can get the colors which you like in https://www.materialui.co/colors
 */
const newColors = ['#FAFAFA', '#BBDEFB', '#64B5F6', '#1E88E5', '#0D47A1']

// Default color of Github
let oldColors = ['#ebedf0', '#c6e48b', '#7bc96f', '#239a3b', '#196127']

const fuckGraphActivities = color => {
  let rects = document.getElementsByTagName('rect')
  let legends = document.getElementsByClassName('legend')

  if (legends[0]) {
    let result = legends[0].getElementsByTagName('li')
    for (let i = 0; i < result.length; i++) {
      result[i].style.backgroundColor = color[i]
    }
  }
  for (let i = 0, length = rects.length; i < length; i++) {
    let fill = rects[i].getAttribute('fill')
    for (let x = 0, y = oldColors.length; x < y; x++) {
      if (fill === oldColors[x]) {
        rects[i].style.fill = color[x]
      }
    }
  }
}

const hex = x => ('0' + parseInt(x).toString(16)).slice(-2)

const rgb2hex = rgb => {
  rgb = rgb.match(/^rgb\((\d+),\s*(\d+),\s*(\d+)\)$/)
  return '#' + hex(rgb[1]) + hex(rgb[2]) + hex(rgb[3])
}

const fuckContributionActivity = color => {
  let activityListing = document.getElementById('js-contribution-activity')
  if (activityListing) {
    let progress = document.getElementsByClassName('progress-bar')
    for (let i = 0, length = progress.length; i < length; i++) {
      // progress[i].style.backgroundColor => RGB color
      // So, must pass to hex color
      let backgroundColor = rgb2hex(progress[i].style.backgroundColor)
      for (let x = 0, y = oldColors.length; x < y; x++) {
        if (backgroundColor === oldColors[x]) {
          progress[i].style.backgroundColor = color[x]
        }
      }
    }
  }
}

(function() {
  'use strict'
  fuckGraphActivities(newColors)
  fuckContributionActivity(newColors)
})()
```

4. Save & Enjoy bitch!!!
