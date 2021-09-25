# Okhttp使用总结

## OkHttp概述



## OkHttp接入

### Maven项目接入

```xml
<dependency>
  <groupId>com.squareup.okhttp3</groupId>
  <artifactId>okhttp</artifactId>
  <version>3.11.0</version>
</dependency>
```

### Gradle接入

```xml
dependencies{
	、、、
	implementation 'com.squareup.okhttp3:okhttp:3.11.0'
	、、、
}
```

## OkHttp简单使用

### GET请求

```java
//获取OKHttp客户端的实例
OkHttpClient okHttpClent = new OkHttpClient();
//构建一个OkHttp请求
Request request = new Rquest.Builder()
    	.get()
    	.url(String url)
    	.build();
//通过OkHttp客户端实例发起Call
Call call = okHttpClient.newCall(request);
//异步发起请求
call.enqueue(new Callback() {
            @Override
    		//失败的回调
            public void onFailure(@NotNull Call call, @NotNull IOException e) {
                e.printStackTrace();
            }

            @Override
    		//成功的回调
            public void onResponse(@NotNull Call call, @NotNull Response response) throws IOException {
                if (response.isSuccessful()) {
                    String result = response.body().string();
                }
            }
        });
```



## Okhttp封装