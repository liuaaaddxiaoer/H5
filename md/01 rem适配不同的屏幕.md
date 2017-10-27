1.  h5中的单位有 px, %, em, rem, 其中 px % em 都不能很好的适配
不同尺寸的屏幕 rem 能动态的改变空间的尺寸


2. em 就是相对于父元素的fontsize的尺寸大小
 例如如果父元素的fontSize的大小是14px;注意谷歌浏览器最低12px
 那么子元素中1em就是 14px, 10em就是 10*14 px
 
3. rem是元素相对于html的fontSize属性来计算的
  如果html的fontSize是20px 那么元素的2rem就是 
  2 * 20 px了。
4.  因此我们可以动态改变html的fontSize属性

4.1 
```

```