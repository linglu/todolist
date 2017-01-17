

2017年 01月 10日 星期二 09:53:59 CST

权限检测流程：
```
// 如果存在某权限
if (checkSelfPermission("")) {
  // ...
} else {
  // 如果不存在某权限，则请求申请权限；
  requestPermissions(String[] pers, REQUEST_CODE;
}
```

```
void onRequestPermissionsResult(int code, String[] pers, int[] grantResults) {
  if (code == REQUEST_CODE) {
    
  }
}
```





