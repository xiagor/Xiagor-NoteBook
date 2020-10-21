## 我家云实习总结

### vue的set方法

项目中使用索引直接更新数组中的值，vue是不能监测这种改变，要用vue的set方法去改变该值。

`this.$set(需要修改的对象，对象的key，赋值给对象key的value值)`



### components文件夹和views文件夹的区别

components是小组件、views是页面级组件，也就是说，views是页面级组件，components是小组件，小组件可被引用在views中，一般views组件不被复用。



