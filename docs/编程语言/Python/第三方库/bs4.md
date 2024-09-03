# BS4
`beautifulsoup4` 是一个非常流行的 Python 库，用于从 HTML 和 XML 文件中提取数据。它能够解析网页内容，并提供简单易用的 API 来访问和处理这些数据。

1. **安装 BeautifulSoup4**：
   ```bash
   pip install beautifulsoup4
   ```

2. **基本用法**：
   ```python
   from bs4 import BeautifulSoup
   import requests

   # 发送 HTTP 请求获取网页内容
   response = requests.get('https://example.com')
   content = response.text

   # 解析网页内容
   soup = BeautifulSoup(content, 'html.parser')

   # 查找网页中的标题
   title = soup.title.string
   print(f"网页标题: {title}")

   # 查找所有的链接
   for link in soup.find_all('a'):
       print(link.get('href'))
   ```

3. **解析和提取数据**：
   ```python
   # 查找特定的标签
   h1_tags = soup.find_all('h1')
   for tag in h1_tags:
       print(tag.text)

   # 查找特定的 ID
   element = soup.find(id='specific-id')
   print(element.text)
   ```