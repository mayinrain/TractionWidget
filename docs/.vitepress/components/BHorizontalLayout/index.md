# BHorizontalLayout
用于提供通用型水平布局

## 组件注册

```js
import { BHorizontalLayout } from '@fesjs/traction-widget';
app.use(BHorizontalLayout);
```
## 代码演示
### 基础用法
传入菜单列表数据，自动生成左侧为菜单栏的水平布局

--USE

--CODE


### 设置默认菜单项全部展开

--USEEXPANDALL


## 参数说明
### BHorizontalLayout Props
| 属性  | 说明                   | 类型                                    |  默认值                                 |是否必须|
| ----- | ----------------------------- | ---------------------------------------- |------------------ |----- |
| curPath | 当前路径 | String|''| 是
| menus | 菜单列表 | Array(object)|[]| 是
| defaultExpandAll | 是否默认展开全部菜单，当curPath有值时，defaultExpandAll将失效 | boolean|false| 否
| isFoot | 是否展示页脚 | Boolean|true| 否
| footText | 页脚内容 | String|WeDataSphere版权所有| 否

### BHorizontalLayout Events
| 事件名称          | 说明                                                                                                                                            | 回调参数                                |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| menuChange | 菜单切换时触发的回调函数                                                                                                                                          | 当前菜单路径值                       |
| sideBarCollapse | 侧边栏折叠展开时触发的回调函数                                                                                                                                          | 当前是否展开菜单，true-折叠，false-展开                   |
### BHorizontalLayout Slots
| 名称          | 说明                                                                                                                                            | 参数                                |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| top | 菜单头部内容                                                                                                                                          | -                        |
| container | 布局右侧主要内容                                                                                                                          | -                        |
## 注意事项
1. BHorizontalLayout为根元素，组件会占满屏幕高度。
2. 布局组件，html的height为100%。
3. 菜单支持根据路径匹配到根菜单进行展开，根菜单需配置路径value