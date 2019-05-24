# vue-tabs

 把tabs复制到项目中


### 引入tabs组件

```
import TabPane from "path/tabs/tab-pane"
import Tabs from "path/tabs/tabs"
```

### 这样使用

```
 <tabs activeName="a" @tab-click="handleClick">
   <tab-pane label="tab1" name="a">tab1</tab-pane>
   <tab-pane label="tab2" name="b">tab2</tab-pane>
   <tab-pane label="tab3" name="c">tab3</tab-pane>
   <tab-pane label="tab4" name="d">tab4</tab-pane>
 </tabs>
```