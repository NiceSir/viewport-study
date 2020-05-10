# sass-study

## 变量声明——$

    <--按照全局或局部变量区分-->
    $a:1px;

## scss与sass后缀名

* sass后缀名的文件中，不能出现大括号或分号
* scss后缀名文件没有进行规则限制

## 父元素符号&

    .main{
        .img{
            color:#ccc;
            &:hover{
                color:#aaa;
            }
        }
    }

## @at-root跳出嵌套层级

        .foo {
        @at-root .bar {
            color: gray;

            @at-root button{
                color:red;

                @at-root span {
                    color: orange;
                }
            }
        }
    }

## 特殊变量——#{$val}

    $width:width;
    #{$width}:300px;

## 控制语句

* @if、@else、@else if
* @for $val from 1 to 3——（1-2）
* @for $val from 1 through 3——（1-3）
* @each $val in a,b,c——a,b,c当作数组存入$val中并遍历
* @each $keys $vals in (h1:2em,h2:1.5em,h3:1em)——键值对遍历

## @mixin——混合

    @mixin reset{
        margin:0;
        padding:0;
    }
    html,body,p1,div{
        @include reset();//引入
    }

    //带参数
    @mixin reset($width,$height){
        width:$width;
        height:$height;
    }
    div{
        @include reset(300px,200px);
    }

## @function——返回值的函数

    @function reset($a){
        return $a+12px;
    }

## @import——导入

## 项目的构建

* 安装sass

```shell
　　
npm install node-sass --save-dev

npm install sass-loader --save-dev

　　# 如果网络不好，会导致安装失败，这时需要从淘宝镜像安装node-sass,

　　npm install -g cnpm --registry=https://registry.npm.taobao.org  （安装淘宝镜像）

　　cnpm install node-sass  --save （使用淘宝镜像安装node-sass）
```
 

* 配置sass编译

　　打开根目录下build/webpack.base.config.js，在modules对象的rules数组中加入一个对象，如下：

```js
module: {
    rules: [
        {
            test: /\.sass$/,
            loaders: ['style', 'css', 'sass']
        }
    ]
}
```

* 配置sass全局变量

有一个babel插件可以完美的解决这个问题：`sass-resources-loader`可以访问sass资源任何一个需要访问的sass模块。所以，可以使用共享变量和混合所有SASS样式，而不去每个文件都引用。

    ```
    npm install --save-dev sass-resources-loader
    ```
然后在 build 文件夹下找到 `util.js` 修改`sass`编译器loader的配置，直接把下面的代码复制进去即可：

```
// 全局文件引入 当然只想编译一个文件的话可以省去这个函数
    function resolveResource(name) {
    return path.resolve(__dirname, '../src/style/' + name);
    }
    function generateSassResourceLoader() {
    var loaders = [
        cssLoader,
        'sass-loader',
        {
        loader: 'sass-resources-loader',
        options: {
            // 多个文件时用数组的形式传入，单个文件时可以直接使用 path.resolve(__dirname, '../static/style/common.scss'
            resources: [resolveResource('theme.scss')]  
        }
        }
        ];
        if (options.extract) {
        return ExtractTextPlugin.extract({
            use: loaders,
            fallback: 'vue-style-loader'
        })
        } else {
        return ['vue-style-loader'].concat(loaders)
        }
    }
```

将默认的sass配置改为 `generateSassResourceLoader()`

```
return {
    css: generateLoaders(),
    postcss: generateLoaders(),
    less: generateLoaders('less'),
    // vue-cli默认sass配置
    // sass: generateLoaders('sass', { indentedSyntax: true }), 
    // scss: generateLoaders('sass'),
    // 新引入的sass-resources-loader
    sass: generateSassResourceLoader(),
    scss: generateSassResourceLoader(),
    stylus: generateLoaders('stylus'),
    styl: generateLoaders('stylus')
  }
```
改完配置后重启服务就可以在`theme.scss`里定义全局变量并在页面中引用了。引用变量的时候直接引用变量名即可。