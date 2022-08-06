# Puppeteer

## Getting React / Vue pages

[node.js - puppeteer await page.$$('.className'), but I get only the first 11 element with that class, why? - Stack Overflow](https://stackoverflow.com/questions/61176809/puppeteer-await-page-classname-but-i-get-only-the-first-11-element-with)

It's probably because the contents of rest of those elements are loaded dynamically with a Javascript framework like React or Vue. This means that it only gets loaded when those elements enter the viewport of the browser.

To fix this you will need to write a function that auto scrolls the page so that those elements can get into the viewport and then you have to wait for that function to finish before you collect the data.

The scrolling function:

```javascript
const autoScroll = async(page) => {
    await page.evaluate(async () => {
        await new Promise((resolve, reject) => {
            var totalHeight = 0;
            var distance = 100;
            var timer = setInterval(() => {
                var scrollHeight = document.body.scrollHeight;
                window.scrollBy(0, distance);
                totalHeight += distance;

                if(totalHeight >= scrollHeight){
                    clearInterval(timer);
                    resolve();
                }
            }, 30);
        });
    });
}
```

Then call this function **after** `page.goto()` and **before** you grab the content with `page.content()`. I also set the viewport width and height then the scrolling goes a little faster:

```javascript
await page.goto(url, {waitUntil: 'load'});
await page.setViewport({
    width: 1200,
    height: 800
});
await autoScroll(page); // The scroll function
const html = await page.content()
```
