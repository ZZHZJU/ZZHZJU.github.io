# request
`requests` 库是一个用于发送 HTTP 请求的 Python 库，常用于与 Web 服务器进行交互。它提供了简单易用的 API，能够处理各种 HTTP 请求，包括 GET、POST、PUT、DELETE 等。

以下是 `requests` 库的基本用法：

1. **安装 `requests` 库**：
   如果还没安装，可以通过 pip 安装：
   ```bash
   pip install requests
   ```

2. **发送 GET 请求**：
   ```python
   import requests
   
   response = requests.get('https://api.example.com/data')
   print(response.text)  # 打印响应内容
   ```

3. **发送 POST 请求**：
   ```python
   import requests
   
   data = {'key': 'value'}
   response = requests.post('https://api.example.com/data', data=data)
   print(response.text)  # 打印响应内容
   ```

4. **设置请求头**：
   ```python
   import requests
   
   headers = {'Authorization': 'Bearer YOUR_TOKEN'}
   response = requests.get('https://api.example.com/data', headers=headers)
   print(response.text)  # 打印响应内容
   ```

5. **处理 JSON 数据**：
   ```python
   import requests
   
   response = requests.get('https://api.example.com/data')
   json_data = response.json()  # 解析 JSON 数据
   print(json_data)
   ```

6. **处理超时和错误**：
   ```python
   import requests
   
   try:
       response = requests.get('https://api.example.com/data', timeout=5)
       response.raise_for_status()  # 如果响应码不是 200，会抛出异常
       print(response.text)
   except requests.exceptions.RequestException as e:
       print(f"请求错误: {e}")
   ```