---
title: "MDN_0X0001: HTML5 CHEAT SHEET"
date: "2023-10-29"
categories: 
  - "code-learning"
  - "learn-html-seriously-from-scratch"
tags: 
  - "cheat-sheet"
  - "html"
coverImage: "724a141e9ffd4a519b9d582151f1c54d.png"
---

# MDN 0X0001 HTML5 CHEAT SHEET

# 1\. ELEMENTS

- [`<a>`](#a): creates a hyperlink to web pages.
- [`<abbr>`](#abbr): represents an abbreviation or acronym.
- [`<acronym>`](#acronym): indicate a sequence of characters that compose an acronym or abbreviation for a word.
- [`<address>`](#address): indicates that the enclosed HTML provides contact information for a person or people, or for an organization.
- [`<area>`](#area): defines an area inside an image map that has predefined clickable areas.
- [`<article>`](#article): represents a self-contained composition in a document, page, application, or site, which is intended to be independently distributable or reusable.
- [`<aside>`](#aside): represents a portion of a document whose content is only indirectly related to the document's main content.
- [`<audio>`](#audio): used to embed sound content in documents.
- [`<b>`](#b)
- [`<base>`](#base)
- [`<bdi>`](#bdi)
- [`<bdo>`](#bdo)
- [`<big>`](#big)
- [`<blockquote>`](#blockquote)
- [`<body>`](#body)
- [`<br>`](#br)
- [`<button>`](#button)
- [`<canvas>`](#canvas)
- [`<caption>`](#caption)
- [`<center>`](#center)
- [`<cite>`](#cite)
- [`<code>`](#code)
- [`<col>`](#col)
- [`<colgroup>`](#colgroup)
- [`<data>`](#data)
- [`<datalist>`](#datalist)
- [`<dd>`](#dd)
- [`<del>`](#del)
- [`<details>`](#details)
- [`<dfn>`](#dfn)
- [`<dialog>`](#dialog)
- [`<dir>`](#dir)
- [`<div>`](#div)
- [`<dl>`](#dl)
- [`<dt>`](#dt)
- [`<em>`](#em)
- [`<embed>`](#embed)
- [`<fieldset>`](#fieldset)
- [`<figcaption>`](#figcaption)
- [`<figure>`](#figure)
- [`<font>`](#font)
- [`<footer>`](#footer)
- [`<form>`](#form)
- [`<frame>`](#frame)
- [`<frameset>`](#frameset)
- [`<h1>`](#h1)
- [`<head>`](#head)
- [`<header>`](#header)
- [`<hgroup>`](#hgroup)
- [`<hr>`](#hr)
- [`<html>`](#html)
- [`<i>`](#i)
- [`<iframe>`](#iframe)
- [`<image>`](#image)
- [`<img>`](#img)
- [`<input>`](#input)
- [`<ins>`](#ins)
- [`<kbd>`](#kbd)
- [`<label>`](#label)
- [`<legend>`](#legend)
- [`<li>`](#li)
- [`<link>`](#link)
- [`<main>`](#main)
- [`<map>`](#map)
- [`<mark>`](#mark)
- [`<marquee>`](#marquee)
- [`<menu>`](#menu)
- [`<menuitem>`](#menuitem)
- [`<meta>`](#meta)
- [`<meter>`](#meter)
- [`<nav>`](#nav)
- [`<nobr>`](#nobr)
- [`<noembed>`](#noembed)
- [`<noframes>`](#noframes)
- [`<noscript>`](#noscript)
- [`<object>`](#object)
- [`<ol>`](#ol)
- [`<optgroup>`](#optgroup)
- [`<option>`](#option)
- [`<output>`](#output)
- [`<p>`](#p)
- [`<param>`](#param)
- [`<picture>`](#picture)
- [`<plaintext>`](#plaintext)
- [`<portal>`](#portal)
- [`<pre>`](#pre)
- [`<progress>`](#progress)
- [`<q>`](#q)
- [`<rb>`](#rb)
- [`<rp>`](#rp)
- [`<rt>`](#rt)
- [`<rtc>`](#rtc)
- [`<ruby>`](#ruby)
- [`<s>`](#s)
- [`<samp>`](#samp)
- [`<script>`](#script)
- [`<search>`](#search)
- [`<section>`](#section)
- [`<select>`](#select)
- [`<slot>`](#slot)
- [`<small>`](#small)
- [`<source>`](#source)
- [`<span>`](#span)
- [`<strike>`](#strike)
- [`<strong>`](#strong)
- [`<style>`](#style)
- [`<sub>`](#sub)
- [`<summary>`](#summary)
- [`<sup>`](#sup)
- [`<table>`](#table)
- [`<tbody>`](#tbody)
- [`<td>`](#td)
- [`<template>`](#template)
- [`<textarea>`](#textarea)
- [`<tfoot>`](#tfoot)
- [`<th>`](#th)
- [`<thead>`](#thead)
- [`<time>`](#time)
- [`<title>`](#title)
- [`<tr>`](#tr)
- [`<track>`](#track)
- [`<tt>`](#tt)
- [`<u>`](#u)
- [`<ul>`](#ul)
- [`<var>`](#var)
- [`<video>`](#video)
- [`<wbr>`](#wbr)
- [`<xmp>`](#xmp)

## 1.1 ELEMENTS INTRODUCTION

## a

### example

```html
<p>You can reach Michael at:</p>

<ul>
  <!-- link -->
  <li><a href="https://example.com">Website</a></li>
  <!-- mail -->
  <li><a href="mailto:m.bluth@example.com">Email</a></li>
  <!-- phone -->
  <li><a href="tel:+123456789">Phone</a></li>
  <!-- linking to relative urls -->
  <a href="//example.com">Scheme-relative URL</a>
  <a href="/en-US/docs/Web/HTML">Origin-relative URL</a>
  <a href="./p">Directory-relative URL</a>
  <!-- linking to an element on the same page -->
  <!-- <a> element links to the section below -->
  <p><a href="#Section_further_down">Jump to the heading below</a></p>
  <!-- heading to link to -->
  <h2 id="Section_further_down">Section further down</h2>
</ul>
```

### using the download attribute to save a `<canvas>` as a PNG

```html
<style>
  html {
    font-family: sans-serif;
  }
  canvas {
    background: #fff;
    border: 1px dashed;
  }
  a {
    display: inline-block;
    background: #69c;
    color: #fff;
    padding: 5px 10px;
  }
</style>

<p>
  Paint by holding down the mouse button and moving it.
  <a href="" download="my_painting.png">Download my painting</a>
</p>
<canvas width="300" height="300"></canvas>

<script type="text/javascript">
  const canvas = document.querySelector("canvas");
  const c = canvas.getContext("2d");
  c.fillStyle = "hotpink";
  let isDrawing;

  function draw(x, y) {
    if (isDrawing) {
      c.beginPath();
      c.arc(x, y, 10, 0, Math.PI * 2);
      c.closePath();
      c.fill();
    }
  }

  canvas.addEventListener("mousemove", (event) =>
    draw(event.offsetX, event.offsetY),
  );
  canvas.addEventListener("mousedown", () => (isDrawing = true));
  canvas.addEventListener("mouseup", () => (isDrawing = false));

  document
    .querySelector("a")
    .addEventListener(
      "click",
      (event) => (event.target.href = canvas.toDataURL()),
    );
</script>
```

### link that opens a new tab/window

```html
<a target="_blank" href="https://www.wikipedia.org">
  Wikipedia (opens in new tab)
</a>
```

### link to a non-html resource

```html
<a href="2017-annual-report.ppt">2017 Annual Report (PowerPoint)</a>
```

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, phrasing content, interactive content, palpable content. |
| Permitted content | Transparent, except that no descendant may be interactive content or an a element, and no descendant may have a specified tabindex attribute. |
| Tag omission | None, both the starting and ending tag are mandatory. |
| Permitted parents | Any element that accepts phrasing content, or any element that accepts flow content, but not other `<a>` elements. |
| Implicit ARIA role | link when href attribute is present, otherwise generic |
| Permitted ARIA roles | When href attribute is present: button,checkbox,menuitem,menuitemcheckbox,menuitem,radio,option,radio,switch,tab,treeitem. When href attribute is not present: any |
| DOM interface | HTMLAnchorElement |

## abbr

### example

```html
<p>
  You can use <abbr>CSS</abbr> (Cascading Style Sheets) to style your
  <abbr>HTML</abbr> (HyperText Markup Language). Using style sheets, you can
  keep your <abbr>CSS</abbr> presentation layer and <abbr>HTML</abbr> content
  layer separate. This is called "separation of concerns."
</p>
```

### providing an expansion

```html
<p>Ashok's joke made me <abbr title="Laugh Out Loud">LOL</abbr> big time.</p>
```

### defining an abbreviation

```html
<p>
  <dfn id="html"><abbr title="HyperText Markup Language">HTML</abbr> </dfn> is a
  markup language used to create the semantics and structure of a web page.
</p>

<p>
  A <dfn id="spec">Specification</dfn> (<abbr>spec</abbr>) is a document that
  outlines in detail how a technology or API is intended to function and how it
  is accessed.
</p>
```

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, phrasing content, palpable content |
| Permitted content | Phrasing content |
| Tag omission | None, both the starting and ending tag are mandatory. |
| Permitted parents | Any element that accepts phrasing content |
| Implicit ARIA role | No corresponding role |
| Permitted ARIA roles | Any |
| DOM Interface | HTMLElement |

## acronym

### example

```html
<p>
  The <acronym title="World Wide Web">WWW</acronym> is only a component of the
  Internet.
</p>
```

## address

### example

```html
<p>Contact the author of this page:</p>

<address>
  <a href="mailto:jim@rock.com">jim@rock.com</a><br />
  <a href="tel:+13115552368">(311) 555-2368</a>
</address>

<address>
  You can contact author at
  <a href="http://www.somedomain.com/contact">www.somedomain.com</a>.<br />
  If you see any bugs, please
  <a href="mailto:webmaster@somedomain.com">contact webmaster</a>.<br />
  You may also want to visit us:<br />
  Mozilla Foundation<br />
  331 E Evelyn Ave<br />
  Mountain View, CA 94041<br />
  USA
</address>
```

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, palpable content. |
| Permitted content | Flow content, but with no nested `<address>` element, no heading content (`<hgroup>`, h1, h2, h3, h4, h5, h6), no sectioning content (`<article>`,`<aside>`, `<section>`, `<nav>`), and no `<header>` or `<footer>` element. |
| Tag omission | None, both the starting and ending tag are mandatory. |
| Permitted parents | Any element that accepts flow content, but always excluding `<address>` elements (according to the logical principle of symmetry, if `<address>` tag, as a parent, can not have nested `<address>` element, then the same `<address>` content can not have `<address>` tag as its parent). |
| Implicit ARIA role | group |
| Permitted ARIA roles | Any |
| DOM interface | HTMLElement Prior to Gecko 2.0 (Firefox 4), Gecko implemented this element using the HTMLSpanElement interface |

## area

### example

```html
<style>
  img {
    display: block;
    margin: 0 auto;
    width: 260px;
    height: 260px;
  }
</style>
<map name="infographic">
  <area
    shape="poly"
    coords="129,0,260,95,129,138"
    href="https://developer.mozilla.org/docs/Web/HTTP"
    target="_blank"
    alt="HTTP"
  />
  <area
    shape="poly"
    coords="260,96,209,249,130,138"
    href="https://developer.mozilla.org/docs/Web/HTML"
    target="_blank"
    alt="HTML"
  />
  <area
    shape="poly"
    coords="209,249,49,249,130,139"
    href="https://developer.mozilla.org/docs/Web/JavaScript"
    target="_blank"
    alt="JavaScript"
  />
  <area
    shape="poly"
    coords="48,249,0,96,129,138"
    href="https://developer.mozilla.org/docs/Web/API"
    target="_blank"
    alt="Web APIs"
  />
  <area
    shape="poly"
    coords="0,95,128,0,128,137"
    href="https://developer.mozilla.org/docs/Web/CSS"
    target="_blank"
    alt="CSS"
  />
</map>
<img
  usemap="#infographic"
  src="/media/examples/mdn-info.png"
  alt="MDN infographic"
/>
```

### attributes

| name | desc |
| --- | --- |
| [coords](#coords) | details the coordinates of the `shape` attribute in size,shape,and placement of an `<area>`. |

#### coords

| name | desc |
| --- | --- |
| rect | the value is `x1,y1,x2,y2`.The value specifies the coordinates of the top-left and bottom-right corner of the rectangle. |
| circle | the value is `x,y,radius`, Value specifies the coordinates of the circle center and the radius. |
| poly | the value is `x1,y1,x2,y2,...,xn,yn`.Value specifies the coordinates of the edges of the polygon. |

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, phrasing content. |
| Permitted content | None; it is a void element. |
| Tag omission | Must have a start tag and must not have an end tag. |
| Permitted parents | Any element that accepts phrasing content. The `<area>` element must have an ancestor `<map>`, but it need not be a direct parent. |
| Implicit ARIA role | link when href attribute is present, otherwise generic. |
| Permitted ARIA roles | No role permitted |
| DOM interface | HTMLAreaElement |

## article

### example

```html
<style>
  .forecast {
    margin: 0;
    padding: 0.3rem;
    background-color: #eee;
  }

  .forecast > h1,
  .day-forecast {
    margin: 0.5rem;
    padding: 0.3rem;
    font-size: 1.2rem;
  }

  .day-forecast {
    background: right/contain content-box border-box no-repeat
      url("/media/examples/rain.svg") white;
  }

  .day-forecast > h2,
  .day-forecast > p {
    margin: 0.2rem;
    font-size: 1rem;
  }
</style>

<article class="forecast">
  <h1>Weather forecast for Seattle</h1>
  <article class="day-forecast">
    <h2>03 March 2018</h2>
    <p>Rain.</p>
  </article>
  <article class="day-forecast">
    <h2>04 March 2018</h2>
    <p>Periods of rain.</p>
  </article>
  <article class="day-forecast">
    <h2>05 March 2018</h2>
    <p>Heavy rain.</p>
  </article>
</article>
```

## aside

### example

```html
<style>
  aside {
    width: 40%;
    padding-left: 0.5rem;
    margin-left: 0.5rem;
    float: right;
    box-shadow: inset 5px 0 5px -5px #29627e;
    font-style: italic;
    color: #29627e;
  }

  aside > p {
    margin: 0.5rem;
  }
</style>

<p>
  Salamanders are a group of amphibians with a lizard-like appearance, including
  short legs and a tail in both larval and adult forms.
</p>

<aside>
  <p>The Rough-skinned Newt defends itself with a deadly neurotoxin.</p>
</aside>

<p>
  Several species of salamander inhabit the temperate rainforest of the Pacific
  Northwest, including the Ensatina, the Northwestern Salamander and the
  Rough-skinned Newt. Most salamanders are nocturnal, and hunt for insects,
  worms and other small creatures.
</p>
```

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, sectioning content, palpable content. |
| Permitted content | Flow content. |
| Tag omission | None, both the starting and ending tag are mandatory. |
| Permitted parents | Any element that accepts flow content. Note that an `<aside>` element must not be a descendant of an `<address>` element. |
| Implicit ARIA role | complementary. |
| Permitted ARIA roles | feed, none, note, presentation, region, search |
| DOM interface | HTMLElement |

## audio

### example

```html
<figure>
  <figcaption>Listen to the T-Rex:</figcaption>
  <audio controls src="/media/cc0-audio/t-rex-roar.mp3">
    <a href="/media/cc0-audio/t-rex-roar.mp3"> Download audio </a>
  </audio>
</figure>
```

### `<audio>` element with `<source>` element

```html
<!-- This example specifies which audio track to embed using the src attribute on a nested <source> element rather than directly on the <audio> element. -->

<audio controls>
  <source src="foo.wav" type="audio/wav" />
  <a href="foo.wav">Download WAV audio</a>.
</audio>
```

### `<audio>` with multiple `<source>` elements

```html
<!-- The browser tries to load the first source element (Opus) if it is able to play it; if not it falls back to the second (Vorbis) and finally back to MP3: -->

<audio controls>
  <source src="foo.opus" type="audio/ogg; codecs=opus" />
  <source src="foo.ogg" type="audio/ogg; codecs=vorbis" />
  <source src="foo.mp3" type="audio/mpeg" />
</audio>
```

### Attributes

| name | desc |
| --- | --- |
| autoplay | Automatically playback the media |
| controls | The browser will offer controls to allow the user to control audio playback, including volume, seeking, and pause/resume playback. |
| controlslist | Helps the browser select what controls to show for the audio element whenever the browser shows its own set of controls.The allowed values are `nodownload`,`nofullscreen` and `noremoteplayback` |
| disableremoteplayback | A Boolean attribute used to disable the capability of remote playback in devices that are attached using wired (HDMI, DVI, etc.) and wireless technologies (Miracast, Chromecast, DLNA, AirPlay, etc.) |
| loop | A Boolean attribute: if specified, the audio player will automatically seek back to the start upon reaching the end of the audio. |
| muted | A Boolean attribute that indicates whether the audio will be initially silenced. Its default value is false. |
| preload | This enumerated attribute is intended to provide a hint to the browser about what the author thinks will lead to the best user experience. The allowd values are `none`,`metadata`,`auto` ,default was `auto` |
| src | The URL of the audio to embed. |

### Events

| Event name | Fired when |
| --- | --- |
| audioprocess | The input buffer of a ScriptProcessorNode is ready to be processed. |
| canplay | The browser can play the media, but estimates that not enough data has been loaded to play the media up to its end without having to stop for further buffering of content. |
| canplaythrough | The browser estimates it can play the media up to its end without stopping for content buffering. |
| complete | The rendering of an OfflineAudioContext is terminated. |
| durationchange | The duration attribute has been updated. |
| emptied | The media has become empty; for example, this event is sent if the media has already been loaded (or partially loaded), and the HTMLMediaElement.load method is called to reload it. |
| ended | Playback has stopped because the end of the media was reached. |
| loadeddata | The first frame of the media has finished loading. |
| loadedmetadata | The metadata has been loaded. |
| loadstart | Fired when the browser has started to load the resource. |
| pause | Playback has been paused. |
| play | Playback has begun. |
| playing | Playback is ready to start after having been paused or delayed due to lack of data. |
| ratechange | The playback rate has changed. |
| seeked | A seek operation completed. |
| seeking | A seek operation began. |
| stalled | The user agent is trying to fetch media data, but data is unexpectedly not forthcoming. |
| suspend | Media data loading has been suspended. |
| timeupdate | The time indicated by the currentTime attribute has been updated. |
| volumechange | The volume has changed. |
| waiting | Playback has stopped because of a temporary lack of data |

### technical summary

|  |  |
| --- | --- |
| Content categories | Flow content, phrasing content, embedded content. If it has a controls attribute: interactive content and palpable content. |
| Permitted content | If the element has a src attribute: zero or more  elements followed by transparent content that contains no
or media elements.Else: zero or more  elements followed by zero or more  elements followed by transparent content that contains no

or media elements.



 |
| Tag omission | None, both the starting and ending tag are mandatory. |
| Permitted parents | Any element that accepts embedded content. |
| Implicit ARIA role | No corresponding role |
| Permitted ARIA roles | application |
| DOM interface | HTMLAudioElement |

## b

## base

## bdi

## bdo

## big

## blockquote

## body

## br

## button

## canvas

## caption

## center

## cite

## code

## col

## colgroup

## data

## datalist

## dd

## del

## details

## dfn

## dialog

## dir

## div

## dl

## dt

## em

## embed

## fieldset

## figcaption

## figure

## font

## footer

## form

## frame

## frameset

## h1

## head

## header

## hgroup

## hr

## html

## i

## iframe

## image

## img

## input

## ins

## kbd

## label

## legend

## li

## link

## main

## map

## mark

## marquee

## menu

## menuitem

## meta

## meter

## nav

## nobr

## noembed

## noframes

## noscript

## object

## ol

## optgroup

## option

## output

## p

## param

## picture

## plaintext

## portal

## pre

## progress

## q

## rb

## rp

## rt

## rtc

## ruby

## s

## samp

## script

## search

## section

## select

## slot

## small

## source

## span

## strike

## strong

## style

## sub

## summary

## sup

## table

## tbody

## td

## template

## textarea

## tfoot

## th

## thead

## time

## title

## tr

## track

## tt

## u

## ul

## var

## video

## wbr

## xmp

# 2\. GLOBAL ATTRIBUTES

- [`accesskey`](#accesskey)
- [`autocapitalize`](#autocapitalize)
- [`autofocus`](#autofocus)
- [`class`](#class)
- [`contenteditable`](#contenteditable)
- [`contextmenu`](#contextmenu)
- [`data-*`](#data)
- [`dir`](#dir)
- [`draggable`](#draggable)
- [`enterkeyhint`](#enterkeyhint)
- [`exportparts`](#exportparts)
- [`hidden`](#hidden)
- [`id`](#id)
- [`inert`](#inert)
- [`inputmode`](#inputmode)
- [`is`](#is)
- [`itemid`](#itemid)
- [`itemprop`](#itemprop)
- [`itemref`](#itemref)
- [`itemscope`](#itemscope)
- [`itemtype`](#itemtype)
- [`lang`](#lang)
- [`nonce`](#nonce)
- [`part`](#part)
- [`popover`](#popover)
- [`slot`](#slot)
- [`spellcheck`](#spellcheck)
- [`style`](#style)
- [`tabindex`](#tabindex)
- [`title`](#title)
- [`translate`](#translate)
- [`virtualkeyboardpolicy`](#virtualkeyboardpolicy)

## 2.1 GLOBAL ATTRIBUTES INTRODUCTION

## accesskey

## autocapitalize

## autofocus

## class

## contenteditable

## contextmenu

## data-\*

## dir

## draggable

## enterkeyhint

## exportparts

## hidden

## id

## inert

## inputmode

## is

## itemid

## itemprop

## itemref

## itemscope

## itemtype

## lang

## nonce

## part

## popover

## slot

## spellcheck

## style

## tabindex

## title

## translate

## virtualkeyboardpolicy

# 3\. ATTRIBUTES

- [`accept`](#accept)
- [`autocomplete`](#autocomplete)
- [`capture`](#capture)
- [`crossorigin`](#crossorigin)
- [`dirname`](#dirname)
- [`disabled`](#disabled)
- [`elementtiming`](#elementtiming)
- [`for`](#for)
- [`max`](#max)
- [`maxlength`](#maxlength)
- [`min`](#min)
- [`minlength`](#minlength)
- [`multiple`](#multiple)
- [`pattern`](#pattern)
- [`placeholder`](#placeholder)
- [`readonly`](#readonly)
- [`rel`](#rel)
- [`required`](#required)
- [`size`](#size)
- [`step`](#step)

## 3.1 ATTRIBUTES INTRODUCTION

## accept

## autocomplete

## capture

## crossorigin

## dirname

## disabled

## elementtiming

## for

## max

## maxlength

## min

## minlength

## multiple

## pattern

## placeholder

## readonly

## rel

## required

## size

## step

# 4\. INPUT TYPES

- [`<input type="button">`](#input_type_button)
- [`<input type="checkbox">`](#input_type_checkbox)
- [`<input type="color">`](#input_type_color)
- [`<input type="date">`](#input_type_date)
- [`<input type="datetim]e-local">`](#input_type_datetime-local)
- [`<input type="email">`](#input_type_email)
- [`<input type="file">`](#input_type_file)
- [`<input type="hidden">`](#input_type_hidden)
- [`<input type="image">`](#input_type_image)
- [`<input type="month">`](#input_type_month)
- [`<input type="number">`](#input_type_number)
- [`<input type="password">`](#input_type_password)
- [`<input type="radio">`](#input_type_radio)
- [`<input type="range">`](#input_type_range)
- [`<input type="reset">`](#input_type_reset)
- [`<input type="search">`](#input_type_search)
- [`<input type="submit">`](#input_type_submit)
- [`<input type="tel">`](#input_type_tel)
- [`<input type="text">`](#input_type_text)
- [`<input type="time">`](#input_type_time)
- [`<input type="url">`](#input_type_url)
- [`<input type="week">`](#input_type_week)

## 4.1 INPUT TYPES INTRODUCTION

## input\_type\_button

## input\_type\_checkbox

## input\_type\_color

## input\_type\_date

## input\_type\_datetime-local

## input\_type\_email

## input\_type\_file

## input\_type\_hidden

## input\_type\_image

## input\_type\_month

## input\_type\_number

## input\_type\_password

## input\_type\_radio

## input\_type\_range

## input\_type\_reset

## input\_type\_search

## input\_type\_submit

## input\_type\_tel

## input\_type\_text

## input\_type\_time

## input\_type\_url

## input\_type\_week
