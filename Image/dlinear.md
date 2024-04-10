#  dlinear

![image-20240409130846348](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409130846348.png)

![image-20240409130908103](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409130908103.png)



```python 
class moving_avg(nn.Module):
    """
    Moving average block to highlight the trend of time series
    """
    def __init__(self, kernel_size, stride):
        super(moving_avg, self).__init__()
        self.kernel_size = kernel_size
        self.avg = nn.AvgPool1d(kernel_size=kernel_size, stride=stride, padding=0)

    def forward(self, x):
        # padding on the both ends of time series
        front = x[:, 0:1, :].repeat(1, (self.kernel_size - 1) // 2, 1)
        end = x[:, -1:, :].repeat(1, (self.kernel_size - 1) // 2, 1)
        x = torch.cat([front, x, end], dim=1)
        x = self.avg(x.permute(0, 2, 1))
        x = x.permute(0, 2, 1)
        return x
```

MSE=0.4 MAE=0.39 var=412

![image-20240409135623794](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409135623794.png)

![image-20240409135634969](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409135634969.png)

# informer

![image-20240409135003908](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409135003908.png)

![image-20240409135852754](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409135852754.png)

![image-20240409140602989](C:\Users\一曲流年\AppData\Roaming\Typora\typora-user-images\image-20240409140602989.png)