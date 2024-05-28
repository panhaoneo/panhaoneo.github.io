+++
title = 'Cpp编码转换'
date = 2024-05-21T16:51:26+08:00
draft = false
+++

1. c99 函数库
```cpp
#include <iostream>
#include <assert.h>
#include <string>
#include <fstream>
#include <stdlib.h>
#include <locale.h>

#ifdef _WIN32
#define CSET_GBK        "936"
#define CSET_UTF8       "65001"
#define LC_NAME_zh_CN   "Chinese_People's Republic of China"
#else
#define CSET_GBK        "GBK"
#define CSET_UTF8       "UTF-8"
#define LC_NAME_zh_CN   "zh_CN"
#endif

#define LC_NAME_zh_CN_GBK       LC_NAME_zh_CN "." CSET_GBK
#define LC_NAME_zh_CN_UTF8      LC_NAME_zh_CN "." CSET_UTF8

bool Gb2312utf8(int i, const std::string &src, std::string &utfstr) {
    if (setlocale(LC_ALL, "zh_CN.gbk") == NULL) {
        std::cout << "setlocale failed, param is bad" << std::endl;
        return false;
    }

    int unicode_len = mbstowcs(NULL, src.c_str(), 0);
    if (unicode_len < 0) {
        std::cout <<"index:" << i << ";"<< src << " cann't transfer" << " ret:" << unicode_len << std::endl;
        return false;
    }
    wchar_t *unicode_str = (wchar_t*)calloc(sizeof(wchar_t), unicode_len+1);
    mbstowcs(unicode_str, src.c_str(), src.size());

    if (setlocale(LC_ALL, "zh_CN.utf8") == NULL) {
        std::cout << "setlocale failed, param is bad" << std::endl;
        return false;
    }
    char utf8_buf[1024] = {0};
    wcstombs(utf8_buf, unicode_str, 1024);
    free(unicode_str);
    utfstr = std::string(utf8_buf);
    return true;
}
```

缺点是需要设置locale，windows的locale设置有问题，名字也很奇怪。

2.  linux使用iconv，windows使用win32的接口
```cpp
#ifdef _WIN32
#include <windows.h>

int GbkToUtf8(char* src_str, size_t src_len, char *dst_str, size_t dst_len) {
    //int len = MultiByteToWideChar(CP_ACP, 0, src_str, -1, NULL, 0);
    wchar_t wstr[src_len * 2];
    memset(wstr, 0, src_len * 2);
    if(MultiByteToWideChar(CP_ACP, 0, src_str, -1, wstr, src_len*2) == 0) {
        int err = GetLastError();
        switch(err) {
            case ERROR_INSUFFICIENT_BUFFER:
                std::cout << "buff not enough." << std::endl; break;
            case ERROR_NO_UNICODE_TRANSLATION:
                std::cout << "invalid unicode" << std::endl; break;
            default: break;
        }
    }
    memset(dst_str, 0, dst_len);
    return WideCharToMultiByte(CP_UTF8, 0, wstr, -1, dst_str, dst_len, NULL, NULL);
}

string Utf8ToGbk(const char* src_str) {
    int len = MultiByteToWideChar(CP_UTF8, 0, src_str, -1, NULL, 0);
    wchar_t* wszGBK = new wchar_t[len + 1];
    memset(wszGBK, 0, len * 2 + 2);
    MultiByteToWideChar(CP_UTF8, 0, src_str, -1, wszGBK, len);
    len = WideCharToMultiByte(CP_ACP, 0, wszGBK, -1, NULL, 0, NULL, NULL);
    char* szGBK = new char[len + 1];
    memset(szGBK, 0, len + 1);
    WideCharToMultiByte(CP_ACP, 0, wszGBK, -1, szGBK, len, NULL, NULL);
    string strTemp(szGBK);
    if (wszGBK) delete[] wszGBK;
    if (szGBK) delete[] szGBK;
    return strTemp;
}

#else
#include <iconv.h>

int GbkToUtf8(char *str_str, size_t src_len, char *dst_str, size_t dst_len) {
    iconv_t cd;
    char **pin = &str_str;
    char **pout = &dst_str;

    cd = iconv_open("utf8", "gbk");
    if (cd == 0) return -1;
    memset(dst_str, 0, dst_len);
    if (iconv(cd, pin, &src_len, pout, &dst_len) == -1) return -1;
    iconv_close(cd);
    **pout = '\0';

    return 0;
}

int Utf8ToGbk(char *src_str, size_t src_len, char *dst_str, size_t dst_len) {
    iconv_t cd;
    char **pin = &src_str;
    char **pout = &dst_str;

    cd = iconv_open("gbk", "utf8");
    if (cd == 0) return -1;
    memset(dst_str, 0, dst_len);
    if (iconv(cd, pin, &src_len, pout, &dst_len) == -1) return -1;
    iconv_close(cd);
    **pout = '\0';

    return 0;
}

#endif

```

3. 编码检测
[BYVoid](https://github.com/BYVoid)/**[uchardet](https://github.com/BYVoid/uchardet)**

