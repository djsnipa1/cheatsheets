# Scriptable

## Forum post [Suggested Approach?](http://talk.automators.fm/t/suggested-approach/7507)

[vaughan.hale](https://talk.automators.fm/u/vaughan.hale) June 17, 2020, 8:21am

*Suggested Approach?*

> I am trying to create a shortcut/script/automation that:
> - calls and API
> - displays the results in a similar way to a tableview (which has a couple action buttons on each row)
> - when a button is selected continues on with the shortcut (or runs a different shortcut) passing the selected rows details.
> Has anyone done anything similar or got any suggestions.

[schl3ck](https://talk.automators.fm/u/schl3ck) June 17, 2020, 10:33am

> Hi!
> - You can make API calls with[`Request`](https://docs.scriptable.app/request)
> - You can build a table in Scriptable with the[`UITable`](https://docs.scriptable.app/uitable), [`UITableRow`](https://docs.scriptable.app/uitablerow) and [`UITableCell`](https://docs.scriptable.app/uitablecell) classes. Don’t forget to call [`table.present()`](https://docs.scriptable.app/uitable/#-present) (where `table` is the instance variable of the `UITable` class) after you’re done building it to present it to the user.
> - To make buttons use either`let btn = row.addButton("caption")` (where row is the UITableRow instance of the current row you are building) or

```javascript
let btn = new UITableCell.button("caption")
row.addCell(btn)
```
and then assign your callback function to [`btn.onTap`](https://docs.scriptable.app/uitablecell/#ontap).

In the callback function you can do whatever you like. If you want to run a shortcut use

```javascript
Safari.open("shortcuts://run-shortcut?name=" + encodeURIComponent("your shortcut name here") + "&input=" + "your data here in your favourite string format (base64, json, URL encoded,...)")

```

(If you want to transfer the word “clipboard” to shortcuts, you have to write `"&input=text&text="` instead of `"&input="`. It seems that this isn’t documented anywhere, but it was like that 2 years ago. If you don’t do it like that, shortcuts will use the contents of the clipboard as input)

An example table:

```javascript
let table = new UITable();
// define contents of an example table
let data = [
	["foo", "bar", "baz"],
	["asdf", "quz", "42"],
	[123, 567, "add"]
];

let row, cell;
let first = true;
for (const drow of data) { // drow = data row
	// create a new row
	row = new UITableRow();
	// immediately add it to the table to not forget that part
	table.addRow(row);
	if (first) {
		// set the first row to have bold text
		row.isHeader = true;
		first = false;
	}
	for (const [i, dcell] of drow.entries()) {
		// the last cell should contain a button
		if (i === 2) {
			// cast dcell to a string, otherwise we will get an error like "Expected value of type UITableCell but got value of type null."
			cell = row.addButton("" + dcell);
			// even though the next line is not needed because it is the default setting, I like to do it anyway to be more specific of what is going on
			cell.dismissOnTap = false;
			// register our callback function
			cell.onTap = () => {
				// create a simple alert to have some user feedback on button tap
				let alert = new Alert();
				alert.message = dcell;
				alert.present();
				// no need to add buttons, they will be added automatically
				// no need to await it, because we don't need anything from the user
			};
		} else {
			// cast dcell to a string, otherwise we will get an error like "Expected value of type UITableCell but got value of type null."
			cell = row.addText("" + dcell);
		}
		cell.centerAligned();
	}
}
table.present();
```

I can’t give you more advice because that depends on your specific case.

[vaughan.hale](https://talk.automators.fm/u/vaughan.hale) June 17, 2020, 11:06am

> Thank you so much for your detailed reply. I will take this a have a good at applying it all tomorrow. Can you tell me if you can do much styling to rows and cells etc?

[schl3ck](https://talk.automators.fm/u/schl3ck)
June 17, 2020, 10:28pm
#4

According to the docs the only styling available is

- separators between rows ( `UITable.showSeparators`)
- regular or bold font ( `UITableRow.isHeader`)
- background color of each row
- height of each row
- space between the cells in one row ( `UITableRow.cellSpacing`)
- relative width of cells (to each other in the same row:` UITableCell.widthWeight`)
- color of text (not buttons)
- alignment of cells

If you for example want a separator between multiple rows to create something like sections without showing separators between every row, you can set the background color of a row to black and it’s height to something small (like 2 or 3, just experiment with it).

If you need more styling options, then you can make the table in HTML with custom CSS and display that in a `WebView`.

- [Home](http://talk.automators.fm/)
- [Categories](http://talk.automators.fm/categories)
- [FAQ/Guidelines](http://talk.automators.fm/guidelines)
- [Terms of Service](http://talk.automators.fm/tos)
- [Privacy Policy](http://talk.automators.fm/privacy)

Powered by [Discourse](https://www.discourse.org), best viewed with JavaScript enabled

