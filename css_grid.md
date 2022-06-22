# CSS Grid

## `.grid-container` 
The main class container

`display: grid` is the main property needed here

### `grid-template-columns`
layout of columns horizontally

`grid-template-columns: 1fr 1fr 1fr` has 3 columns, each one is `1fr`

A shorthand would be `grid-template-columns: repeat(3, 1fr);`

### `grid-template-rows`
is the same as `grid-template-columns` only vertically

### `justify-items`
How grid pieces are aligned horizontally

`justify-items: strech;` is default and takes up full width of the columns
`justify-items: center;` centers grid items 
`justify-items: start;` pushes grid items to the left
`justify-items: end;` pushes grid items to the right

> **IMPORTANT**

To justify individual grid items, you must use `justify-self`

`justify-self: end;` will align grid item to the bottom of it's grid area

### `align-items` 
Like `justify-items` but vertical

> **IMPORTANT**

`align-self` for vertical alignment of grid items

### `gap` is the gap between grid items
`gap: 10px;`
 
--- 

## Grid Items

### `grid-column`
Helps lay out the grid

`grid-column: 1 / span 2;` will make this grid item 1 column and span 2 column spaces

> **_See image and code below_** 

---

![css grid](https://i.imgur.com/8CMKw37.png)

```html
<body>
  <div class="grid-container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div> 
  </div>
 ```

 ```css
body {
  margin: 30px;
  font-family: "Poppins";
}

.grid-container {
  background: #eee;
  max-width: 900px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: 100px 200px 300px;
  gap: 10px;
  justify-items: strech;
  align-items: strech;
}

.grid-container > div {
  background: #ccc;
  text-align: center;
  padding: 20px;
  border: 1px solid #000;
}

.grid-container > div:nth-child(1) {
  grid-column: 1 / span 2;
}
.grid-container > div:nth-child(2) {
  grid-column: 3 / span 3;
}
.grid-container > div:nth-child(3) {
  grid-column: span 1;
}
.grid-container > div:nth-child(4) {
  grid-column: 2 / 6; 
  align-self: end;
}
.grid-container > div:nth-child(5) {
  grid-column: span 3; 
}
.grid-container > div:nth-child(6) {
  grid-column: span 3; 
  justify-self: end;
  align-self: start;
}
```
