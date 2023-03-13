```dataviewjs
let seachString = dv.current()["search-tag"] + " and #type/book"
let pages = dv.pages(seachString)

if (pages.length != 0) {
	dv.table(["Buch"], pages.map(k => [k.file.link]))
}
```