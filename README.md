# 圓錐曲線實作 – 圓錐曲線和極座標方程式
- 作者（Author）：姜名孺（Ming-Ju Chiang）
- 以下為小論文「離」不「圓」了的研究內容，在 Jupyter Notebook 的環境下，以 Python 程式繪製出不同離心率下，極座標方程式呈現的圓錐曲線圖形。

## 1. 圓錐曲線和極座標方程式
Define  $F(0, 0)$ is a fixed point ; $L:x = 3$ is a fixed line ; $P$ is a moving point on the plot of conic section , the polar coordinate of $P$ is $[r, \theta]$. $e$ is the eccentricity of the plot which $P$ forms, $d=d(F, L)=3$.

Use the equation and the moving point $P\ $:

<p align="center">
<a href="[https://www.codecogs.com/eqnedit.php?latex=x_s(t)=\sum_{n}x_c(nT)\delta(t-nT)](https://latex.codecogs.com/svg.image?&space;r=\frac{ed}{1&plus;e\cdot&space;cos\mathit{\theta}},(0\leq\mathit{\theta}\leq&space;2\pi);\mathit{P[r,\theta]}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?r=\frac{ed}{1&plus;e\cdot&space;cos\mathit{\theta}},(0\leq\mathit{\theta}\leq&space;2\pi);\mathit{P[r,\theta]}" title="polar equation" /></a>
</p>

to demonstrate the plot of conic section.
```python
%matplotlib inline
%config InlineBackend.figure_format = 'svg'
import numpy as np
import matplotlib.pyplot as plt
```
```python
def conic_section_plot(e): # e--> Eccentricity(離心率)
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
- 因為在 Github 線上瀏覽 Jupyter Notebook 的程式碼和執行結果時，不會顯示 interact 這個函式的執行結果，所以我將其操作過程及成果展示拍成影片，在後面附上影片連結。使用 Github 線上瀏覽程式碼時，連結下面的圖片是使用 interact 這函式的執行結果的截圖。
### [interact 函式執行結果的影片連結](https://youtu.be/-5KLJwPNfdM)

### 以下為 e（Eccentricity, 離心率）在各個區間中的圓錐曲線圖形
### 1.1 點 (e = 0)
![image](https://github.com/user-attachments/assets/3012cf5d-3cd0-4669-86c2-986b704ce845)

### 1.2 橢圓 (0 < e < 1, e = 0.9)
![image](https://github.com/user-attachments/assets/9099b453-5e08-4a0a-8ab9-a62fa16a9d4b)

### 1.3 拋物線 (e = 1)
![image](https://github.com/user-attachments/assets/13c8b580-9e8a-4220-8d18-8a559bb1e190)

### 1.4 雙曲線 (e > 1, e = 1.5)
![image](https://github.com/user-attachments/assets/e8ec8c86-012d-4121-8013-f4ad5035eab3)

### 附錄：GeoGebra 圓錐曲線極座標方程式 (線上互動版）
[]("https://www.geogebra.org/classic/gf6vub8h?embed")
