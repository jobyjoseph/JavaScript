Create a new folder `pwa`.

`index.html`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Live Cricket Score</title>
    <link href="css/style.css" rel="stylesheet" />
  </head>
  <body>
    <header>
      Live Cricket
    </header>
    <div class="container">
      <div>Score:</div>
      <div id="score">0/0</div>
    </div>
  </body>
</html>

```

Initial  `css/style.css`:
```css
html,
body {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  background: #eee;
}

header {
  height: 60px;
  line-height: 60px;
  text-align: center;
  background: #4056d6;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
}

.container {
  text-align: center;
  margin: 100px auto;
  font-size: 18px;
}

#score {
  font-size: 60px;
  font-weight: bold;
}


```

create `store.json`
```js
{
  "score": "243/2"
}
```

add jQuery reference
```html
<script
      src="https://code.jquery.com/jquery-3.3.1.min.js"
      integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
      crossorigin="anonymous"
    ></script>
```

`js/app.js`
```js
$(document).ready(function() {
  setInterval(function() {
    $.ajax({
      url: "score.json",
      success: function(data) {
        $("#score").text(data.score);
      }
    });
  }, 5000);
});
```
Add reference to `js/app.js`


## App Shell
