# 使用eslint+prettier规范前端代码风格

## eslint

可组装的JavaScript和JSX检查工具

- [eslint中文官网](https://cn.eslint.org/)

eslint配置文件可以是写在package.json里， 也可以是.eslintrc或是.eslintrc.json.

## prettier

### Prettier 是什么？

虽然js没有官方推荐的代码规范，不过社区有些比较热门的代码规范，比如standardjs、airbnb。
使用ESLint配合这些规范，能够检测出代码中的潜在问题，提高代码质量，但是并不能完全统一代码风格，
因为这些代码规范的重点并不在代码风格上。

Prettier的中文意思是“漂亮的、机灵的”，也是一个流行的代码格式化工具的名称，它能够解析代码，使用你自己设定的规则来重新打印出格式规范的代码。

Prettier具有以下几个有优点：

- 可配置化
- 支持多种语言
- 集成多数的编辑器
- 简洁的配置项

## 安装

使用yarn安装：

```
yarn add prettier --dev --exact
# 或全局安装
yarn global add prettier
```

用npm安装

```
npm install --save-dev --save-exact prettier
# or globally
npm install --global prettier
```

## Pre-commit Hook

让我们能够在提交代码（git add）的之前使用Prettier自动格式化我们的代码。

```
yarn add lint-staged husky --dev
```

然后在package.json中加上以下配置

```
{
	"husky": {
		"hooks": {
			"pre-commit": "lint-staged"
		}
	},
	"lint-staged": {
		"*.{js, json, css, md}": ["prettier --write", "git add"]
	}
}
```

[具体使用可以点击查看](https://prettier.io/docs/en/precommit.html)


## ESLint 与 Prettier配合使用

### 安装

```
// 首先， 我们需要安装 prettier, eslint
// 然后我们需要支持提交代码自动格式化代码，需要安装husky lint-staged
// 我们需要eslint与eslint配置， 所以需要安装eslint-plugin-prettier插件

yarn add --dev prettier husky lint-staged eslint eslint-plugin-prettier
```

1. 在package.json加上上面pre-commit hook的配置

2. 添加.eslintrc配置文件

```
{
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```

3. 添加.prettierrc配置文件

```
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": false,
  "singleQuote": true
}
```

如果在vscode中使用prettier,请安装  Prettier - Code formatter 插件。

至此：

- 在vscode中按下alt+shift+f 键就可以自动格式代我们的代码了。
- 在git add 提交了时候也会自动格式化我们的代码。
- 在vscode, eslint也会提示出错的信息

### 如果prettier配置和已存在的eslint插件冲突怎么办？

```
yarn add --dev eslint-config-prettier
```
通过使用eslint-config-prettier配置，能够关闭一些不必要的或者是与prettier冲突的lint选项。这样我们就不会看到一些error同时出现两次。使用的时候需要确保，这个配置在extends的最后一项。


```
// .eslintrc改为
{
  "extends": [
	  "standard" // 使用standard做代码规范
	  "prettier"
  ],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error"
  }
}
```


### eslint 常用的代码规范

- eslint-config-standard  [连接](https://www.npmjs.com/package/eslint-config-standard) [中文文档](https://standardjs.com/readme-zhcn.html)
- eslint-config-airbnb [连接](https://www.npmjs.com/package/eslint-config-airbnb)
- eslint-config-alloy [AlloyTeam ESLint 规则](https://www.npmjs.com/package/eslint-config-alloy)


### 附， Prettier 配置选项

1. printWidth  
> 设置prettier单行输出（不折行）的（最大）长度。
> 
> 出于代码的可读性，我们不推荐（单行）超过80个字符的coding方式。

2. tabWidth
> 设置工具每一个水平缩进的空格数, 默认为2

3. useTabs
> 使用tab（制表位）缩进而非空格； 默认: false

4. semi
> 在语句末尾添加分号；默认：true
>
> - true - 在每一条语句后面添加分号
> - false - 只在有可能导致ASI错误的行首添加分号

5. singleQuote
> 使用单引号而非双引号；默认值： false
> - 在JSX语法中，所有引号均为双引号，该设置在JSX中被自动忽略
> - 在字符串中，如果一种引号在数量上超过另一种引号，数量少的引号，将被用于格式化字符串；示例："I 'm double quoted "被格式化后是："I 'm double quoted "(我觉得这里好像有点问题，但是亲测例子结果就是这样，按理说被较少使用的是单引号，但是例子就是双引号包裹的，尊重原文吧) ；再例："This \"example\" is single quoted "格式化过后：'This "example" is single quoted '

6. trailingCommas
> 在任何可能的多行中输入尾逗号。 尾逗号[a,b,c,d,] 数组项d后面的逗号就是尾逗号。 
> - none  - 无尾逗号；
> - es5  - 添加es5中被支持的尾逗号；
> - all  - 所有可能的地方都被添加尾逗号；（包括函数参数），这个参数需要安装nodejs8或更高版本；

7. bracketSpacing
> 在对象字面量声明所使用的的花括号后（{）和前（}）输出空格
> - true - Example: {   foo: bar  }
> - false - Example: {foo: bar}

8. jsxBracketSameLinte
> 在多行JSX元素最后一行的末尾添加 > 而使 > 单独一行（不适用于自闭和元素）
> - true  -  > 单独起一行
> - false -  > 接下属性后面

9. alwaysParens
> 为单行箭头函数的参数添加圆括号。
> - " avoid " - 尽可能不添加圆括号，示例：x => x
> - " always " - 总是添加圆括号，示例： (x) => x

10. parser
> 指定使用哪一种解析器。
> 
> babylon和flow都支持同一套JavaScript特性（包括Flow）.Prettier将自动根据文件的输入路径选择解析器，如非必要，不要修改该项设置。

11. filePath
> 指定文件的输入路径，这将被用于解析器参照。

12. requirePragma
13. insertPragma
14. proseWrap