# Regex Expression
正则表达式用于匹配目标字符串，许多语言都提供了正则表达式语法，在 C++ 中，你可以使用 <regex> 头文件提供的正则表达式库来处理正则表达式。
## Simple Example
``` cpp
std::regex pattern("[0-9]+"); // 匹配一个或多个数字
std::string text = "12345";
if (std::regex_match(text, pattern)) {
    std::cout << "匹配成功！" << std::endl;
} else {
    std::cout << "匹配失败！" << std::endl;
}

std::regex pattern("[a-z]+"); // 匹配一个或多个小写字母
std::string text = "Hello123world";
std::smatch matches;
if (std::regex_search(text, matches, pattern)) {
    std::cout << "找到匹配子串：" << matches[0] << std::endl;
}
```

##  Further Application
验证电子邮箱的地址
``` cpp
#include <iostream>
#include <regex>

int main() {
    std::string email = "user@example.com";
    
    // 定义正则表达式模式来匹配电子邮件地址
    std::regex pattern(
        R"((\w+)        // 匹配一个或多个字母、数字或下划线 (用户名的第一部分)
        (\.?\w+)*       // 可选的，匹配".单词" (例如 user.name)
        @               // 匹配 @ 符号
        (\w+\.)+        // 匹配域名部分，至少包含一个 "单词."
        \w+)            // 匹配顶级域名 (例如 .com, .net)
    ");
    
    if (std::regex_match(email, pattern)) {
        std::cout << "有效的电子邮件地址" << std::endl;
    } else {
        std::cout << "无效的电子邮件地址" << std::endl;
    }
    
    return 0;
}
```