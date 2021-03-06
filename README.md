# Webpack handlebars plugin

> Server-side template rendering using [Handlebars](http://handlebarsjs.com/).


`npm install handlebars-webpack-plugin --save-dev`


## Usage

In your webpack config register and setup the handlebars plugin

```javascript
var path = require("path");
var HandlebarsPlugin = require("handlebars-webpack-plugin");

var webpackConfig = {

    plugins: [

        new HandlebarsPlugin({
            // path to main hbs template
            entry: path.join(process.cwd(), "app", "src", "index.hbs"),
            // filepath to result
            output: path.join(process.cwd(), "build", "index.html"),
            // data passed to main hbs template: `main-template(data)`
            data: require("./app/data/project.json"),

            // globbed path to partials, where folder/filename is unique
            partials: [
                path.join(process.cwd(), "app", "src", "components", "*", "*.hbs")
            ],

            // register custom helpers
            helpers: {
                nameOfHbsHelper: Function.prototype,
                path.join(process.cwd(), "app", "helpers", "*.helper.js")
            },

            // hooks
            onBeforeSetup: function (Handlebars) {},
            onBeforeAddPartials: function (Handlebars, partialsMap) {},
            onBeforeCompile: function (Handlebars, templateContent) {},
            onBeforeRender: function (Handlebars, data) {},
            onBeforeSave: function (Handlebars, resultHtml) {},
            onDone: function (Handlebars) {}
        })
    ]
};
```

Partial ids are registered by `parentFolder/filename` (without file extensions)

Use handlebars in your main and partials like, i.e.

```hbs
<body>
    {{> partialFolder/partialName}}

    {{> header/header title="page title"}}

    {{> partial/content}}
</body>
```

