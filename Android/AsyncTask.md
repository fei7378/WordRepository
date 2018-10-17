# 构建AsyncTask子类的参数
```java
- AsyncTask<Params,Progress,Result>是一个抽象类,通常被继承.
```
1. Params: 启动任务时输入参数的类型.
2. Progress: 后台任务执行中返回进度值的类型.
3. Result: 后台执行任务完成后返回结果的类型.
---
## 构建AsyncTask子类的回调方法
1. doInBackground: 必须重写,异步执行后台线程的任务**(必须实现)**
2. onPreExecute: 执行后台耗时操作前调用,完成初始化操作
3. onPostExecute: 当`doInBackground()`完成后,系统自动调用此方法,将doInBackground方法的返回值传递到该方法,在此进行结果展示
4. onProgressUpdate: 在`doInBackground()`方法中调用`publishProgress()`方法更新任务的执行进度后就会触发该方法,可以了解当前耗时操作的完成进度.
