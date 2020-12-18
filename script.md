# Script files

## Script tag

The best practice (2020) is to put `<script>` tags in `<head>` and use the `async` or `defer` attributes: https://stackoverflow.com/questions/436411/where-should-i-put-script-tags-in-html-markup.

The reason for this is that the browser will stop rendering when it encounters a `<script>` tag and wait for the script to download and execute.
The old guidance was to put `<script>` at the end of `<body>` if they aren't needed while the document is loading,
but the page will still end up waiting for the scripts to download and run.

## Bundling and minifying

I looked at what Bootstrap uses: https://github.com/twbs/bootstrap/blob/main/package.json.

Turns out that `uglifyjs` only works on ES2015.
Their recommendation is basically "use Babel."
But, most browsers run >= ES2017 natively, and I'd like to use things like `async` and `yield` (not sure if Babel supports that; I know TypeScript won't handle it).

Bootstrap uses https://github.com/terser/terser.
