# Alias
vector database

## Architecture
![alias_architecture](https://github.com/hunter2009pf/Alias/assets/32154029/ab234943-d2bf-49d3-ba52-f3be406cd6c7)

## Self-questioning
1. How to convert text, images, audios to vectors?
2. How to implement different kinds of similarity search algorithm?
3. How to realize distributed vector database?

## 在Linux上编译基于faiss库的可执行文件遇到的问题
1.c++ standard 11未启用
在CMakeLists.txt文件中添加：
```
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```

2./usr/local/lib64/libfaiss.so: undefined reference to `vtable for std::__cxx11::basic_istringstream<char, std::char_traits<char>, std::allocator<char> >@GLIBCXX_3.4.21'
libstdc++.so库版本过低，需要将本地所有依赖路径中的libstdc++.so替换成最新版本。
首先查看使用的libstdc++.so版本
```
/sbin/ldconfig -p | grep stdc++
        libstdc++.so.6 (libc6,x86-64) => /lib64/libstdc++.so.6
ls -l /lib64/libstdc++.so.6
lrwxrwxrwx. 1 root root 19 Jun  1  2022 /lib64/libstdc++.so.6 -> libstdc++.so.6.0.19
```
使用新版本动态库替换
```
ls -l /usr/lib64/libstdc++.so.6
lrwxrwxrwx. 1 root root 19 Jun  1  2022 /usr/lib64/libstdc++.so.6 -> libstdc++.so.6.0.19
ls -l /usr/local/lib64/libstdc++.so.6
lrwxrwxrwx. 1 root root 19 Aug 28 11:47 /usr/local/lib64/libstdc++.so.6 -> libstdc++.so.6.0.32
cp /usr/local/lib64/libstdc++.so.6 /usr/lib64/
cp: overwrite ‘/usr/lib64/libstdc++.so.6’? yes
```
