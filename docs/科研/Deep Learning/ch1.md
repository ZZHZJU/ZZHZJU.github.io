# PyTorch
## 环境配置
1. **安装 Anaconda**：Anaconda是Python的一个科学计算发行版本
2. **conda拉取PyTorch**:注意版本的兼容性
3. **测试是否安装成功**：去调用一下torch库

## 基础语法

### 张量
在数学里，张量是一种几何实体，或者说广义上的“数量”。张量概念包括标量、向量和线性算子。张量可以用坐标系统来表达，记作标量的数组。标量可以看作零维张量，向量可以看作一维张量，矩阵可以看作二维张量，因此张量又称多维数组(multi dimension array)
``` py
import torch
import numpy as np
z = torch.Tensor(4,5)#生成一个4*5大小的张量
y = torch.rand(4,5)#产生一个四行五列的矩阵
print(z+x)
print(torch.add(z,y))#这两行都是矩阵加法
b = z.numpy()#将Tensor转换为numpy数组
```

### 数学计算
``` py
import torch
torch.abs(torch.FloatTensor([-1,-2,3]))#计算张量每一个元素的绝对值
torch.acos(input,out=None)#返回一个新张量，包含原张量每个元素的反余弦
torch.add(input,value,out=None)#对输入张量逐元素加上标量值value，并返回结果得到的一个新张量out
```

### 数理统计
``` py
import torch
torch.mean(input)#返回输入张量所有元素的平均值
torch.mean(input,dim,out=None)#返回输入张量给定维度dim上每行均值
```
### 比较操作
```py
torch.eq(input,other,out=None)#比较元素相等性，第二个参数可以为一个数与第一个参数同类类型形状的张量
torch.equal(input,other,out=None)#如果两个张量有相同的形状和元素值，则返回True，否则False
torch.ge(input,other,out=None)#逐元素比较input和other是否input>=other
torch.gt(input,other,out=None)#逐元素比较input和other是否input>other
```

## 具体模块

### torch.nn

#### Module 类
Module 是神经网络的基本组成部分，作为一个抽象类，可以通过成员函数实现不同的神经网络结构。
``` py
class Model(nn.Module):
    def __init__(self):
        ### 具体实现
    def forward(self,x):
        ### 具体实现
```

#### Functional 函数
1. **激活函数**：
   - `F.relu(input)`：计算输入的 ReLU 激活函数，$y=\begin{cases}0\qquad x\leq0\\x\qquad x>0
   \end{cases}$
   - `F.sigmoid(input)`：计算输入的 Sigmoid 激活函数,$y=\frac{1}{1+e^{-x}}$，优点是求导容易且优化稳定，缺点是由于其软饱和性，容易产生梯度消失并且输出并不是以零为中心
   - `F.tanh(input)`：计算输入的 Tanh 激活函数,$y=\frac{1-e^{-2x}}{1+e^{-2x}}$，优点是相比Sigmoid函数收敛更快且输出以零为中心，缺点依旧是没有改变由于饱和性产生的梯度消失
   - `F.softmax(input, dim)`：计算输入的 Softmax 函数。

2. **损失函数**：
   - `F.cross_entropy(input, target)`：计算交叉熵损失。
   - `F.mse_loss(input, target)`：计算均方误差损失。
   - `F.binary_cross_entropy(input, target)`：计算二分类交叉熵损失。

3. **卷积操作**：
   - `F.conv1d(input, weight, bias=None, stride=1, padding=0)`：一维卷积操作。
   - `F.conv2d(input, weight, bias=None, stride=1, padding=0)`：二维卷积操作。
   - `F.conv3d(input, weight, bias=None, stride=1, padding=0)`：三维卷积操作。

4. **池化操作**：
   - `F.max_pool2d(input, kernel_size, stride=None, padding=0)`：二维最大池化操作。
   - `F.avg_pool2d(input, kernel_size, stride=None, padding=0)`：二维平均池化操作。

5. **归一化操作**：
   - `F.batch_norm(input, running_mean, running_var, weight=None, bias=None, training=False, momentum=0.1, eps=1e-5)`：批量归一化。
   - `F.layer_norm(input, normalized_shape, weight=None, bias=None, eps=1e-5)`：层归一化。

6. **线性变换**：
   - `F.linear(input, weight, bias=None)`：执行线性变换操作，通常用于全连接层。

7. **其他功能**：
   - `F.dropout(input, p=0.5, training=True)`：应用 Dropout 随机丢弃一些神经元，防止过拟合。
   - `F.interpolate(input, size=None, scale_factor=None, mode='nearest')`：对输入进行插值操作（如上采样）。

#### optim

1. **SGD（随机梯度下降）**：
   - `torch.optim.SGD(params, lr=<学习率>, momentum=0, dampening=0, weight_decay=0, nesterov=False)`
   - 是最基础的优化算法，通过计算梯度来更新模型参数。可以配合 `momentum`（动量）来加速收敛。

2. **Adam（自适应矩估计）**：
   - `torch.optim.Adam(params, lr=<学习率>, betas=(0.9, 0.999), eps=1e-8, weight_decay=0, amsgrad=False)`
   - 一种更复杂的优化算法，结合了动量和自适应学习率。通常在很多深度学习任务中表现优异。

3. **RMSprop（均方根传播）**：
   - `torch.optim.RMSprop(params, lr=<学习率>, alpha=0.99, eps=1e-8, weight_decay=0, momentum=0, centered=False)`
   - 适用于非平稳目标函数，能够自动调整学习率。

4. **Adagrad（自适应梯度算法）**：
   - `torch.optim.Adagrad(params, lr=<学习率>, lr_decay=0, weight_decay=0, eps=1e-10)`
   - 适用于稀疏数据集，能够自动调整每个参数的学习率。

5. **AdamW**：
   - `torch.optim.AdamW(params, lr=<学习率>, betas=(0.9, 0.999), eps=1e-8, weight_decay=0.01, amsgrad=False)`
   - Adam 的一个变种，通过在更新过程中直接施加权重衰减，改进了正则化效果。

6. **Adadelta**：
   - `torch.optim.Adadelta(params, lr=<学习率>, rho=0.9, eps=1e-6, weight_decay=0)`
   - 也是一种自适应学习率优化算法，适合于不同特征尺度的学习。

7. **LBFGS（有限内存 BFGS）**：
   - `torch.optim.LBFGS(params, lr=<学习率>, max_iter=20, max_eval=None, tolerance_grad=1e-5, tolerance_change=1e-9, history_size=100, line_search_fn=None)`
   - 一种基于二阶导数的优化算法，适用于需要精确收敛的场景，通常用于较小规模的优化问题。

#### autograd

1. **`torch.autograd.Variable`**：
   - `Variable` 是张量的一个包装，它持有张量的数据以及梯度。`Variable` 是自动求导的核心概念，但在最新版本的 PyTorch 中，已经直接将 `Tensor` 类本身作为支持自动求导的核心类型，所以直接使用 `Tensor` 即可。

2. **`torch.autograd.grad`**：
   - 计算并返回输入张量的梯度。通常用于需要手动计算梯度的情况。

   ```python
   torch.autograd.grad(outputs, inputs, grad_outputs=None, retain_graph=None, create_graph=False)
   ```

3. **`torch.autograd.backward`**：
   - 执行反向传播，用于计算损失相对于输入张量的梯度。

   ```python
   loss.backward()
   ```

4. **`torch.autograd.Function`**：
   - 自定义求导方法。通过定义 `forward` 和 `backward` 方法，可以自定义前向和反向传播的行为。

   ```python
   class MyFunction(torch.autograd.Function):
       @staticmethod
       def forward(ctx, input):
           ctx.save_for_backward(input)
           return input.clamp(min=0)

       @staticmethod
       def backward(ctx, grad_output):
           input, = ctx.saved_tensors
           grad_input = grad_output.clone()
           grad_input[input < 0] = 0
           return grad_input
   ```

5. **`torch.autograd.no_grad`**：
   - 禁用自动求导。在评估模型或推理时，通常不需要梯度，因此可以用 `no_grad` 来节省内存和计算资源。

   ```python
   with torch.autograd.no_grad():
       output = model(input)
   ```

6. **`torch.autograd.detect_anomaly`**：
   - 在反向传播时检测异常，用于调试梯度爆炸或梯度消失问题。

   ```python
   with torch.autograd.detect_anomaly():
       loss.backward()
   ```

#### save
``` py
import torch

# 假设你有一个 PyTorch 模型
model = MyModel()

# 保存模型的状态字典
torch.save(model.state_dict(), 'model.pth')

# 你也可以保存其他对象，例如张量
tensor = torch.randn(5, 3)
torch.save(tensor, 'tensor.pth')

# 还可以保存多个对象到一个文件
checkpoint = {
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'epoch': epoch
}
torch.save(checkpoint, 'checkpoint.pth')
```

#### cuda

以下是 `torch.cuda` 的一些常用功能：

1. **检查是否有可用的 GPU:**
   ```python
   torch.cuda.is_available()
   ```
   返回 `True` 如果有可用的 GPU，否则返回 `False`。

2. **获取当前 GPU 设备的数量:**
   ```python
   torch.cuda.device_count()
   ```
   返回可用的 GPU 设备数量。

3. **设置当前 GPU 设备:**
   ```python
   torch.cuda.set_device(device)
   ```
   设置当前默认的 GPU 设备，`device` 参数可以是设备的索引号（如 `0`、`1`）。

4. **获取当前 GPU 设备:**
   ```python
   torch.cuda.current_device()
   ```
   返回当前默认的 GPU 设备索引号。

5. **将张量转移到 GPU:**
   ```python
   tensor = tensor.to('cuda')  # 或 tensor.cuda()
   ```
   将 PyTorch 张量转移到 GPU 上以进行计算。

6. **GPU 设备上的内存管理:**
   ```python
   torch.cuda.memory_allocated()
   torch.cuda.memory_reserved()
   ```
   这些函数用于查询 GPU 上的内存使用情况。