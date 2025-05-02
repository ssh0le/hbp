# Webpack

Прежде чем начать работу с webpack, необходимо установить для него необходимые зависимости.

## Зависимости

### React

`react react-dom`

Все зависимости далее устанавливаются в devDependencies.

### Webpack

`webpack webpack-cli webpack-dev-server html-webpack-plugin babel-loader @babel/core @babel/plugin-transform-runtime @babel/preset-env @babel/preset-react @babel/preset-typescript`

### Typescript

`typescript @types/react @types/react-dom`


## Конфигурации

Базовая конфигурация webpack.config.js:
`
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    mode: "development",
    entry: path.resolve(__dirname, "..", "./src/index.tsx"),
    resolve: {
        extensions: [".tsx", ".ts", ".js"],
    },
    module: {
        rules: [
            {
                test: /\.(ts|js)x?$/,
                exclude: /node_modules/,
                use: [
                    {
                        loader: "babel-loader",
                    },
                ],
            },
            {
                test: /\.css$/,
                use: ["style-loader", "css-loader"],
            },
            {
                test: /\.(?:ico|gif|png|jpg|jpeg)$/i,
                type: "asset/resource",
            },
            {
                test: /\.(woff(2)?|eot|ttf|otf|svg|)$/,
                type: "asset/inline",
            },
        ],
    },
    output: {
        path: path.resolve(__dirname, "..", "./build"),
        filename: "bundle.js",
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: path.resolve(__dirname, "..", "./public/index.html"),
        }),
    ],
    stats: "errors-only",
};
`

Здесь нужно обратить внимание на следующие моменты, которые могут быть разными для каждого проекта:
entry - точка входа в приложение, в нашем случае это файл index.tsx
plugins -> HtmlWebpackPlugin template - файл html, куда будет вставляться `<script>` с бандлом