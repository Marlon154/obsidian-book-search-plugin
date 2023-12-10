# Obsidian Book Search Plugin

![GitHub Workflow Status](https://img.shields.io/github/workflow/status/anpigon/obsidian-book-search-plugin/Release%20Obsidian%20plugin?logo=github)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/anpigon/obsidian-book-search-plugin?sort=semver)
[![Korean](https://img.shields.io/badge/Language-한국어-blueviolet)](README.ko.md)

Easily create book notes.

<br>

## Changelog

### [0.5.8](https://github.com/anpigon/obsidian-book-search-plugin/compare/0.5.8-beta.2...0.5.8) (2022-09-13)

### Features

- Add locale selection for Google searches.
- Can use the [Templater plugin](https://github.com/SilentVoid13/Templater) with.
- Enables [Inline scripts](https://github.com/anpigon/obsidian-book-search-plugin#inline-script) for templates.

<br>

## Demo

https://user-images.githubusercontent.com/3969643/184918274-8ad24546-2e01-4288-a855-c8eeb1feca7d.mp4

<br>

## Description

Use to query book using :

- A book title, author, publisher or ISBN (10 or 13).

Use Google Books API to get the book information.

<br>

## How to install

Click the link to install the Book Search plugin: [Install Link](https://obsidian.md/plugins?id=obsidian-book-search-plugin)

Or, Search in the Obsidian Community plugin. And install it.

<img width="700" src="https://user-images.githubusercontent.com/3969643/184918934-585375a9-7b25-4905-81c8-5f092ed74991.png">

<br>

## How to use

### 1. Click the ribbon icon, or excute the command "Create new book note".

<img width="600" src="https://user-images.githubusercontent.com/3969643/161973483-ab007598-e0b8-433f-9697-75ee0ef74195.png">

### 2. Search for books by keywords.

<img width="600" src="https://user-images.githubusercontent.com/3969643/161973979-51f642c9-626a-4015-a7e9-dfdbe6ec2cbc.png">

### 3. Select the book from the search results.

<img width="600" src="https://user-images.githubusercontent.com/3969643/161974310-13c3b39b-51dc-472f-b787-db64f74caf74.png">

### 4. Voila! A note has been created.

<img width="600" src="https://user-images.githubusercontent.com/3969643/161974593-1b7bfe69-cb9d-47d7-a43d-1d725295a122.png">

<br>

## How to use settings

<img width="700"  src="https://user-images.githubusercontent.com/3969643/184919550-68eff0e4-2b02-41bb-8f17-30a5354359a3.png">

### New file location

Set the folder location where the new file is created. Otherwise, a new file is created in the Obsidian Root folder.

### New file name

You can set the file name format. The default format is `{{title}} - {{author}}`.
You can use `{{DATE}}` or `{{DATE:YYYYMMDD}}` to set a unique file name.

### Template file

You can set the template file location. There is an example template at the bottom.

### Service Provider

You can set up the services that you use to search for books. Only Google and Naver(네이버) are available now.
To use Naver Book Search, clientId and clientSecret are required. I will explain how to get clientId and clientSecret from Naver on my blog.

### <strike>(Deprecated) Text to insert into front matter</strike>

<strike>You can add the following to the default Front Matter, or create a new Front Matter with the structure you want.</strike> Please use the template file described below.

### <strike>(Deprecated) Text to insert into content</strike>

<strike>You can add text to the content for [Dataview inline metadata](https://blacksmithgu.github.io/obsidian-dataview/data-annotation/#pages).</strike> Please use the template file described below.

<br>

## Example template

Please also find a definition of the variables used in this template below (see: [Template variables definitions](#template-variables-definitions)).

```
---
tag: 📚Book
title: "{{title}}"
author: [{{author}}]
publisher: {{publisher}}
publish: {{publishDate}}
total: {{totalPage}}
isbn: {{isbn10}} {{isbn13}}
cover: {{coverUrl}}
status: unread
created: {{DATE:YYYY-MM-DD HH:mm:ss}}
updated: {{DATE:YYYY-MM-DD HH:mm:ss}}
---

![cover|150]({{coverUrl}})

# {{title}}

```

<br>

## Dataview rendering

<img width="1024" alt="" src="https://user-images.githubusercontent.com/3969643/184546096-82ccaae6-9893-411b-aed6-a72c54f72cb2.png">

Here is the dataview query used in the demo

````
# 📚 My Bookshelf

```dataview
TABLE WITHOUT ID
	status as Status,
	rows.file.link as Book
FROM  #📚Book
WHERE !contains(file.path, "Templates")
GROUP BY status
SORT status
```

## List of all books

```dataview
TABLE WITHOUT ID
	status as Status,
	"![|60](" + cover + ")" as Cover,
	link(file.link, title) as Title,
	author as Author,
	join(list(publisher, publish)) as Publisher
FROM #📚Book
WHERE !contains(file.path, "Templates")
SORT status DESC, file.ctime ASC
```
````

The banner at the top of the document is rendered using [Obsidian-banners](https://github.com/noatpad/obsidian-banners) plugin.

<br>

## Template variables definitions

Please find here a definition of the possible variables to be used in your template. Simply write `{{name}}` in your template, and replace name by the desired book data, including:

| name        | description                                             |
| ----------- | ------------------------------------------------------- |
| title       | The title of the book.                                  |
| subtitle    | The subtitle of the book.                               |
| author      | The name of the book author. It can be multiple people. |
| category    | Book category.                                          |
| description | Book description.                                       |
| publisher   | The publisher of the book.                              |
| totalPage   | The total number of pages in the book.                  |
| coverUrl    | Book cover image URL.                                   |
| publishDate | The year the book was published.                        |
| isbn10      | ISBN10                                                  |
| isbn13      | ISBN13                                                  |

<br>

## Advanced

You can add the following syntax to your template

### Inline Script

#### If you want to see all the book data in JSON format:

````
```json
<%=book%>
```
````

or

````
```json
<%=JSON.stringify(book, null, 2)%>
```
````

#### When you want to list or link authors:

```
authors: <%=book.authors.map(author=>`\n  - ${author}`).join('')%>
```

or linked:

```
authors: <%=book.authors.map(author => `[[${author}]]`).join(', ')%>
```

<br>

## License

[Obsidian Book Search Plugin](https://github.com/anpigon/obsidian-book-search-plugin) is licensed under the GNU AGPLv3 license. Refer to [LICENSE](https://github.com/SilentVoid13/Templater/blob/master/LICENSE.TXT) for more information.

<br>

## Contributing

Feel free to contribute.

You can create an [issue](https://github.com/anpigon/obsidian-book-search-plugin/issues) to report a bug, suggest an improvement for this plugin, ask a question, etc.

You can make a [pull request](https://github.com/anpigon/obsidian-book-search-plugin/pulls) to contribute to this plugin development.

<br>

## Support

If this plugin helped you and you wish to contribute :)

Buy me coffee on [buymeacoffee.com/anpigon](https://www.buymeacoffee.com/anpigon)

<a href="https://www.buymeacoffee.com/anpigon" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="60"></a>&nbsp;
<a href="https://anpigon.github.io/buymeacoffee/"><img src="https://user-images.githubusercontent.com/3969643/184924261-f0224843-08fa-4bce-af70-dc5db589979f.png" height="60"></a>
