# Matplotlib
Matplotlib 是一个用于 Python 的绘图库，可以生成高质量的图形和可视化结果。它通常用于数据分析和科学计算中。

## 基本用法

1. **安装 Matplotlib**
   你可以通过 pip 安装 Matplotlib：
   ```bash
   pip install matplotlib
   ```

2. **绘制简单图形**
   ```python
   import matplotlib.pyplot as plt

   # 创建数据
   x = [1, 2, 3, 4, 5]
   y = [2, 3, 5, 7, 11]

   # 创建图形和坐标轴
   plt.figure()
   plt.plot(x, y, label='Line Plot')
   
   # 添加标题和标签
   plt.title('Simple Line Plot')
   plt.xlabel('X Axis')
   plt.ylabel('Y Axis')
   
   # 添加图例
   plt.legend()
   
   # 显示图形
   plt.show()
   ```

3. **绘制散点图**
   ```python
   import matplotlib.pyplot as plt

   # 创建数据
   x = [1, 2, 3, 4, 5]
   y = [2, 3, 5, 7, 11]

   # 创建散点图
   plt.scatter(x, y, color='red', label='Scatter Plot')
   
   # 添加标题和标签
   plt.title('Simple Scatter Plot')
   plt.xlabel('X Axis')
   plt.ylabel('Y Axis')
   
   # 添加图例
   plt.legend()
   
   # 显示图形
   plt.show()
   ```

4. **绘制直方图**
   ```python
   import matplotlib.pyplot as plt

   # 创建数据
   data = [1, 2, 2, 3, 4, 4, 4, 5, 5, 6]

   # 创建直方图
   plt.hist(data, bins=6, color='blue', edgecolor='black')
   
   # 添加标题和标签
   plt.title('Simple Histogram')
   plt.xlabel('Bins')
   plt.ylabel('Frequency')
   
   # 显示图形
   plt.show()
   ```

5. **子图**
   ```python
   import matplotlib.pyplot as plt

   # 创建数据
   x = [1, 2, 3, 4, 5]
   y = [2, 3, 5, 7, 11]

   # 创建子图
   fig, axs = plt.subplots(1, 2, figsize=(10, 5))
   
   # 第一个子图
   axs[0].plot(x, y, 'tab:blue')
   axs[0].set_title('Line Plot')
   
   # 第二个子图
   axs[1].scatter(x, y, color='red')
   axs[1].set_title('Scatter Plot')
   
   # 添加整体标题
   plt.suptitle('Subplots Example')
   
   # 显示图形
   plt.show()
   ```

Matplotlib 是一个非常强大的工具，适用于创建各种类型的图形。你可以根据需求自定义各种属性，如颜色、样式、刻度等。