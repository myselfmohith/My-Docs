## Contents

<div style="display: flex;justify-content:space-between" ><h2>Contents</h2><a href="./../README.md"> < back</a></div>

* [Tik Tok Scroll](#tiktok-scroll)

---

### TikTok Scroll
Tiktok scroll is very easy to implement doesn't even need the **javascript**,The CSS feature that enables me to implement is `scroll-snap`

#### Parent
The parent should not be overflowed and set overflow-<direction> to `scroll`.

|Code|Inputs|Notes|
|:-|:-|:-|
|`scroll-snap-type`|`x` or `y`|Snap Direction|
||`manditory`|Always snap the child even when scrolling|
||`proximity`|Only snap when the scrolling is stop|


#### Child
|Code|Inputs|Notes|
|:-|:-|:-|
|`scroll-snap-align`|`start` or `center` or `end`|Snaps the element to respective postion specified|
|`scroll-snap-stop`|`always`|Make sure the snap of the elemnt is done as that of the tiktok only _one element_|

```css
.parent{
    scroll-snap-type: y mandatory;
    /* along vertical scroll with manditory */
    overflow-x: hidden;
    overflow-y: scroll;
}

.child{
    scroll-snap-align: start;
    scroll-snap-stop: always;
    /* Limit scroll to one item on mobile swipe screen  */
}
```