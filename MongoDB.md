
# Sections

<details open="open">
  <summary>Contents table</summary>
  <ol>
    <li>
      <a href="#Change-the-document-root">Change the document root</a>
    </li>
    <li>
      <a href="#Getting-the-current-date">Getting the current date</a>
    </li>
    <li>
      <a href="#Display-de-date-picker">Display de date picker</a>
    </li>
  </ol>
</details>

#Change the document root
> This is really usefull when you want to change document's root, it means if there are any neasted array and toy want to place it as the main "Table" to display you can place it
``` JavaScript
{ $replaceRoot: { newRoot: <replacementDocument> } }
```
