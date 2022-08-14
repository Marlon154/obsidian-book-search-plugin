# Obsidian Book Search Plugin

![GitHub Workflow Status](https://img.shields.io/github/workflow/status/anpigon/obsidian-book-search-plugin/Release%20Obsidian%20plugin?logo=github&style=for-the-badge)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/anpigon/obsidian-book-search-plugin?style=for-the-badge&sort=semver)

Easily create book notes.

## Demo

![May-05-2022 18-01-01](https://user-images.githubusercontent.com/3969643/166892687-d36868ef-f966-41af-9bb1-88e17ea5753f.gif)

If this plugin helped you and you wish to contribute :)

<a href="https://www.buymeacoffee.com/anpigon" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>

<br>

## Description

Use to query book using :

- A book title, author, publisher or ISBN (10 or 13).

Use Google Books API to get the book information.

[블로그: 옵시디언 책 검색 플러그인 사용방법](https://anpigon.tistory.com/165)

<br>

## How to install

Search in the Obsidian Community plugin. And install it.

![](https://user-images.githubusercontent.com/3969643/166097211-abb60f55-3d77-4de6-9e0d-b681f903aafc.png)

<br>

## How to use

1. Set the folder to new file location in plugin options. And you can also add a frontmatter that is inserted when creating a note.
   ![](https://user-images.githubusercontent.com/3969643/162614248-c60baab1-ef26-4f68-bf78-d0bc462e6c41.png)

2. Excute the command "Create new book note".
   ![](https://user-images.githubusercontent.com/3969643/161973483-ab007598-e0b8-433f-9697-75ee0ef74195.png)

3. Search for books by keywords.
   ![](https://user-images.githubusercontent.com/3969643/161973979-51f642c9-626a-4015-a7e9-dfdbe6ec2cbc.png)

4. Select the book from the search results.
   ![](https://user-images.githubusercontent.com/3969643/161974310-13c3b39b-51dc-472f-b787-db64f74caf74.png)

5. Voila! A note has been created.
   ![](https://user-images.githubusercontent.com/3969643/161974593-1b7bfe69-cb9d-47d7-a43d-1d725295a122.png)

<br>

## How to use settings

### <strike>(Deprecated) Text to insert into front matter</strike>

<strike>You can add the following to the default Front Matter, or create a new Front Matter with the structure you want.</strike>

<br>

### <strike>(Deprecated) Text to insert into content</strike>

<strike>You can add text to the content for [Dataview inline metadata](https://blacksmithgu.github.io/obsidian-dataview/data-annotation/#pages).</strike>

<br>

Please use the template file described below.

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
isbn: {{isbn10}} {{isbn1#template-variable-definition
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
| author      | The name of the book author. It can be multiple people. |
| category    | book category                                           |
| publisher   | The publisher of the book.                              |
| totalPage   | The total number of pages in the book.                  |
| coverUrl    | Book cover image URL.                                   |
| publishDate | The year the book was published.                        |
| isbn10      | ISBN10                                                  |
| isbn13      | ISBN13                                                  |

<br>

## License

[Obsidian Book Search Plugin](https://github.com/anpigon/obsidian-book-search-plugin) is licensed under the GNU AGPLv3 license. Refer to [LICENSE](https://github.com/SilentVoid13/Templater/blob/master/LICENSE.TXT) for more information.

<br>

## Contributing

Feel free to contribute.

You can create an [issue](https://github.com/anpigon/obsidian-book-search-plugin/issues) to report a bug, suggest an improvement for this plugin, ask a question, etc.

You can make a [pull request](https://github.com/anpigon/obsidian-book-search-plugin/pulls) to contribute to this plugin development.
