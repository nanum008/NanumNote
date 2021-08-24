# HTML基础

## 常用元素

### Form表单

#### 作用

form标签是专门用来收集用户填写信息的一种标签

#### 示例

```html
<form action="">
    ……
</form>
```

- action属性里填写提交地址(服务器地址)
- form标签里面可以添加很多元素
- 每一个表单元素都要起一个name！！！这个name对应的就是提交的参数名称，用户输入的内容就是参数的值，提交之后会在服务器被解析。

```html
<form action="" method="GET">

        <!-- 单行文本输入框 -->
        用户：<input type="text" name="user"><br>

        <!-- 密码输入框 输入的内容只会被处理在显示，防止他人窥视-->
        密码：<input type="password" name="password"><br>

        <!-- 单选框 -->
        <!-- 使用单选框需要为每一个单选框定义好value属性，每个框对应不同的值，而且每一组单选框的name属性保持一致； -->
        性别：男<input type="radio" name="sex" value="boy"> 女<input type="radio" name="sex" value="girl"><br>

        <!-- 多选框 -->
        爱好：足球<input type="checkbox" name="intrest" value="football">篮球<input type="checkbox" name="intrest"
            value="basketball"><br>

        <!-- 下拉选择框 -->
        城市：<select name="city" id="">
            <option value="001">北京</option>
            <option value="002">上海</option>
            <option value="003">深圳</option>
            <option value="004">广东</option>
        </select><br>

        <!-- 文件提交    让用户选择要上传的文件，这里只是上传文件的名字，若需实现文件的上传，需搭配JS实现 -->
        文件上传：<input type="file"><br>

        <!-- 多行文本输入框 -->
        简介：<textarea name="introduce" id="" cols="30" rows="10"></textarea><br>

        <!-- 提交按钮 向服务器提交用户填写的数据-->
        <input type="submit">

        <!-- 重置按钮 清空用户填写的信息-->
        <input type="reset"><br>
        <hr>

        <!-- 普通按钮 -->
        <input type="button" value="这是一个普通按钮">

        <!-- 图片按钮   图片按钮具有和提交按钮一样的提交功能，在src属性里填写图片的资源路径即可展示图片按钮 -->
        <input type="image" src="这里填写图片资源文件路径">
    </form>
```

