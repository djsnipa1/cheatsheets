# Images in `README.md` Markdown Files

## Image Sizes

### Image source

`https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png`

![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png)

#### Resize it!

**Supposedly this works best on Github**

```markdown
<img src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=50% />

<img src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=“100px” />
```

<img src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=50% />

<img src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=“100px” />

---

`![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png | width=100)`
![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png | width=10)

`![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png =250x250)`
![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png =250x250)

`![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png)`  
  - Copy `<img>` in browser DevTools. Replace `![](url)` to `<img>`. Add width(and height) attr.
  - `<img src=“https://camo.githubusercontent.com/...” data-canonical-src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=“200” height=“400” />`
  - <img src=“https://camo.githubusercontent.com/331400aee821efda2e36ee9b3bc8bce93b975109/68747470733a2f2f6779617a6f2e636f6d2f65623563353734316236613961313663363932313730613431613439633835382e706e67” alt=“” data-canonical-src=“https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png” width=“200” height=“400” />

---

```markdown
<div style=“width: 60%; height: 60%”>
  ![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png)
</div>
```

<div style=“width: 60%; height: 60%”>
  ![](https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png)
</div>

---

## Reference Images

In the body use `![image description][imageName]`. **Note the 2** sets of `[]`.

Now, at the bottom of the document provide the `src` url with the `[imageName]:
`
```markdown
![image description][imageName]

[imageName]: https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png
```
or omit the description…

```markdown
![imageName]

[imageName]: https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png
```

![image description][imageName]

![imageName]

[imageName]: https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png
