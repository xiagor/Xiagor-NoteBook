

## CSS标准盒子模型和IE怪异盒子模型

+ 标准模式下：
  + width是content的宽度
  + 一个块的宽度是width+padding+border+margin
+ 怪异模式下：
  + width包含了content、padding、border的宽度
  + 一个块的宽度是width+margin



## CSS居中问题

### 1. 水平居中

+ 盒子内的文字水平居中：`text-align: center;`（也可以让盒子内的行内元素和行内块居中对齐）
+ 块级盒子水平居中：左右margin改成auto

### 2. 垂直居中

+ 盒子内的文字垂直居中：`line-height=盒子的高度`

+ 块级盒子垂直居中

  + 块级元素高度和宽度已知：绝对定位和负边距

  + 块级元素高度未知：

    + 方法一：使用CSS3的`transform: translateY(-50%);`

    + 方法二：使用flex布局，对容器：（在flex布局中，父元素叫容器，子元素叫项目）

      ```css
      display: flex;
      flex-direction: column;/* 决定主轴的方向的属性，column：主轴为垂直方向，从上往下 */
      justify-content: center;/* 定义了项目在主轴上的对齐方式，center：在主轴居中 */
      ```

## 外边距塌陷

### 1. 相邻块元素垂直外边距的合并

+ 当上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，

+ 则他们之间的垂直间距不是margin-bottom和margin-top之和
+ 而是取两个值中的较大者（外边距合并也称外边距塌陷）





