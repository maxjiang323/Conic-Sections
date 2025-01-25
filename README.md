# 圓錐曲線實作 – 圓錐曲線及極座標參數式（以下內容與 Jupyter Notebook 中的程式碼相同）
下面的實作我分成兩個部分。第一個是以圓錐曲線的「極座標」參數式畫圖，因為在 Github 線上瀏覽 Jupyter Notebook 的程式碼和執行結果時，不支援編譯 interact 這個函式，所以我將其「操作過程」拍成影片附上連結，而使用 Github 線上瀏覽程式碼時，連結下面的圖片僅是使用 interact 這函式的部分程式的執行結果的截圖。
- 註記：前面的假設我全部都用英文來寫

## 1. 圓錐曲線及「極座標」參數式
$r=\frac{ed}{1+e·cos\theta}\ , (0\le\theta\le2\pi)\ , P[r, \theta]$

Use the equation and the moving point $P\;$:
$r=\frac{ed}{1+e·cos\theta}\ , (0\le\theta\le2\pi)\ , P[r, \theta]$
to demonstrate the plot of conic section.
```python
%matplotlib inline
%config InlineBackend.figure_format = 'svg'
import numpy as np
import matplotlib.pyplot as plt
```
```python
def conic_section_plot(e): # e--> Eccentricity(偏心率)
    d = 3 # d --> d(F, L)
    theta = np.arange(0, 2*np.pi, 0.001) 
    r = (e*d)/(1+e*np.cos(theta)) 
    
    # Polar Coordinate(極座標)
    x = r*np.cos(theta) 
    y = r*np.sin(theta) 
    
    if e > 1:
        y[:-1][np.diff(y) < 0] = np.nan
            
    plt.rcParams['figure.figsize'] = (11, 4) # set the size of plot to (11:4)[x, y]
    plt.rcParams.update({'font.size': 14}) # enlarge the size on the numbers of x axis and y axis 
    plt.axis([-30, 40, -10, 10]) # set the limit of x axis and y axis --> [x_min, x_max, y_min, y_max]
    plt.xticks([-30, 0, 3, 40], ['-30', '0','3', '40'])
    plt.axis('on') # plot the axis(x and y)
    plt.grid(True, zorder = 1) # plot the grid
    
    plt.axhline(0, color = 'black', linewidth = 2, zorder = 2) # plot the line of the axis
    plt.axvline(0, color = 'black', linewidth = 2, zorder = 2) # plot the line of the y axis
    plt.scatter(0, 0, color = 'blue', s = 50, zorder = 3, label = r'$F(0, 0)$') 
    # plot the focus point, original setting : (0, 0) (it can be reset)
    plt.plot(x, y,color = 'orange', linewidth = 3, zorder = 3, label = r'$P[r, \theta]$') # The Plot of Conic Section
    plt.axvline(3, color = 'red', linewidth = 3, zorder = 3, label = r'$L:x=3$') # plot the fixed line
    
    plt.title('The Plot of Conic Section', fontsize = 20)
    plt.legend(loc = 'best', fontsize = 14)
```
```python
from ipywidgets import interact
interact(conic_section_plot, e = (0.00, 4.00)) 
# original setting : the e(eccentricity) range from 0.00, 0.10, 0.20, ... , 3.90, 4.00 (it can be reset)
```
### [操作程式碼的影片連結](https://youtu.be/-5KLJwPNfdM)

### 以下各個區間中 e（Eccentricity, 偏心率）的圓錐曲線圖形
### 1.1 e = 0
![image](https://github.com/user-attachments/assets/3012cf5d-3cd0-4669-86c2-986b704ce845)

### 1.2 0 < e < 1

