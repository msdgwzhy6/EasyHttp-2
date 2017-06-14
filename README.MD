EasyHttp 一个可扩展的Http框架
===
一、使用
---
1、 引入项目
compile 'com.liwy.easyhttp:easyhttp:1.0.2'<br/>
2、 初始化
在Application里初始化如下：
```
OkHttpClient okHttpClient = new OkHttpClient.Builder().connectTimeout(10, TimeUnit.SECONDS).build();
OkHttpService okHttpService = new OkHttpService().init(okHttpClient);
EasyHttp.getInstance().setHttpService(okHttpService);
```
或者
```
RetrofitService retrofitService = new RetrofitService().init("http://192.168.131.19:8886/",10);
EasyHttp.getInstance().setHttpService(retrofitService);
```
现实现了两种Http服务，分别是基于OkHttp和Retrofit。<br/>
3、 使用<br/>
get
```
        // 参数
        Map<String,Object> params = new HashMap<>();
        params.put("ver","1");
        new EasyHttp.Builder()
                .setUrl("/login/update")
                .setTag("update")
                .setParams(params)
                .setSuccessCallback(new SuccessCallback<String>() {
                    @Override
                    public void success(String result) {
                        contentTv.setText("Build String = " + result);
                    }})
                .setErrorCallback(new ErrorCallback() {
                    @Override
                    public void error(Object... values) {
                        contentTv.setText("请求失败");
                    }})
                .get();
```

post
```
        // 参数
        Map<String,Object> params = new HashMap<>();
        params.put("ver","1");
        new EasyHttp.Builder()
                .setUrl("/login/update")
                .setTag("update")   //请求的tag，可用于中断请求
                .setParams(params)
                .setSuccessCallback(new SuccessCallback<String>() {
                    @Override
                    public void success(String result) {
                        contentTv.setText("Build String = " + result);
                    }})
                .setErrorCallback(new ErrorCallback() {
                    @Override
                    public void error(Object... values) {
                        contentTv.setText("请求失败");
                    }})
                .post();
```
如果需要在请求过程中取消该请求，可以如下操作：
```
EasyHttp.getInstance().cancelHttp("update");
```
更新日志
---
1.0.3
---
1. 新增下载方法,OkHttpService和RetrofitService均已实现。
2. EasyHttp新增获取Builder的静态方法
    public static Builder getBuilder():
3. 删除无用类
    
1.0.2
---
1. 完善EasyHttp初始化方法
2. 新增Http请求中断功能
3. 修复bug.

1.0.1
---
1. 版本发布至Jcenter.