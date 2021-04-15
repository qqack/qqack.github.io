# Form 布局实现自适应

### 需求

需要根据窗口大小自适应 `Form` 布局

### 实现思路

1. 获取当前窗口大小
2. 定义默认布局
3. 监听窗口变化
4. uesEffect 改变布局

### 代码实现

```ts
// 1.获取当前窗口大小
const getWindowSize = () => ({
  innerHeight: window.innerHeight,
  innerWidth: window.innerWidth,
});
// 2.定义默认布局
const [layout, setLayout] = useState<'horizontal' | 'vertical'>('horizontal');
const formLayout =
  layout === 'horizontal'
    ? {
        labelCol: { sm: { span: 6 }, xl: { span: 10 } },
        wrapperCol: { sm: { span: 4 }, xl: { span: 14 } },
      }
    : {};
// 3.监听窗口变化
const handleResize = () => {
  setWindowSize(getWindowSize());
};

useEffect(() => {
  // 监听
  window.addEventListener('resize', handleResize);
  // 销毁
  return () => window.removeEventListener('resize', handleResize);
}, []);

// 4.uesEffect改变布局
useEffect(() => {
  if (windowSize.innerWidth < 1444) {
    setLayout('vertical');
  } else {
    setLayout('horizontal');
  }
}, [windowSize]);
```

### Form 组件

```html
<form
  className="{styles.propertiesForm}"
  form="{form}"
  onFinish="{submitForm}"
  layout="{layout}"
  {...formLayout}
>
  {renderForm()}
</form>
```
