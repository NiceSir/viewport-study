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
        test: /\.s[ac]ss$/i,
        use: [
          // Creates `style` nodes from JS strings
          'style-loader',
          // Translates CSS into CommonJS
          'css-loader',
          // Compiles Sass to CSS
          'sass-loader',
        ],
      },
    ]
}
```

* 引入外部scss文件
在main.js中引入需要的scss文件