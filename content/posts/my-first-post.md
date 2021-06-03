---
title: "My First Post"
author: "Tommy Dittberner"
date: 2021-05-30T20:05:21+02:00
draft: true
tags: [
"markdown",
"css",
"html",
]
---

This is some content, lol.

# Hello World

## This is a smaller subtitle

#### Code block with Hugo's internal highlight shortcode
{{< highlight html >}}
<!doctype html>
<html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
</html>
{{< /highlight >}}


{{<highlight javascript >}}
renderAnchor = function () {
    for (let num = 1; num <= 6; num++) {
        // search h1-h6
        const headers = document.querySelectorAll('.article-post>h' + num);
        for (let i = 0; i < headers.length; i++) {
            const header = headers[i];
        }
    }
}();
{{< /highlight >}}
