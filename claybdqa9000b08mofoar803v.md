# INLINE, BLOCK-LEVEL, AND INLINE-BLOCK BOXES in CSS

# Block-Level Elements

1. Elements are formatted visually as** blocks**.
2. Elements take up **100% of the parent element's width**, regardless of what's in the content.
3. By default, elements are stacked **vertically**, one after another.

**Default elements**: body, main, header, footer, section, nav, aside, div, h1-h6, p, ul, ol, li, etc.

** With CSS**: display: block


```
//index.html
<p> Hi! I am a block level element </p>
``` 

```
//style.css
p{
background-color:black;
color:white;
}``` 


![Screenshot (45).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669468235392/ho3iydlE6.png align="left")

[Check Live Version Here](https://codepen.io/mrtyagi07/pen/QWxxjRj)

# Inline-Level Elements

1. Takes up only the space **necessary for its content.**
2. Causes no line-breaks after or before the element
3. The box model applies differently. **Heights and widths do not apply.**
4. Paddings and margins are only applied horizontally (left and right).

**Default elements**: a, img, strong, em, button, etc.

**With CSS**: display: inline


```
//index.html

<button class="inline"> Hi! I an inline level element </button>
``` 

```
//style.css

body{
 background-color:aqua;
}
.inline{
  padding-top:50px;
  padding-bottom:50px;
  margin-top:50px;
}``` 


![Screenshot (46).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669469786845/_qVVXJW7R.png align="left")

*Wait, Vaibhav, what did you say in point number 4, but here it's happening the complete opposite?* 

![WhyGradySmithGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1669470076489/lhB13Kq_5.gif align="left")

Let's find out why:

- Most browsers display button elements as inline-block by default. It's worth noting that HTML5 forces them to be displayed as inline-block anyways. <img> is also an example of this.

# Inline-Block-Level Elements

1. Looks inline from the outside, and behaves like block-level on the inside.
2. Occupies only content’s space (**Point 1 from Inline-level**).
3. Causes no line-breaks (**Point 2 from Inline-level**).

**With CSS**: display: inline-block

Follow me on Twitter for updates on my progress and to chat with me about anything and everything. 😇🙂


[Twitter Profile](https://twitter.com/mrtyagi07)