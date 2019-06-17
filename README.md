# create MNIST-A dataset

64x64の黒い背景に変形したMNISTを埋め込んだデータセットを作成します  
コマンドを実行するとpng形式で保存されます  

<p align="left"><img width="20%" src="png/30575.png" /></p>
例えば上のような画像(文字は2，位置xは36，位置yは36，角度は-45，大きさは28)を生成します  
また，同時にラベル[大きさ, sin(角度), cos(角度), 位置X, 位置Y, 文字]も生成します

## option

-n: name  
data以下に置くフォルダ名を決めます  

-i: iteration  
データの量を何倍するかを決めます  

-nl: number  
MNISTのラベルを指定できます  
ex: 0, 1, 2, ..., 9

-pxl: position x  
-pyl: position y  
64x64の黒い背景のどこに画像を貼り付けるかを指定します 
x, y座標それぞれを偶数で指定できます  
ex: 0, 2, 4, 6, ..., 36  

-al: angle  
MNISTの回転の角度を決めます  
ex: 45, 20, 0, -20, ...

-sl: scale  
MNISTの大きさを指定します  
ex: 2, 4, 6, ..., 28  

### example
```
python create_mnist_A.py -n MNIST_A -i 1000 -nl 1,2 -pxl 0,36 -pyl 0,36 -al 45,0,-45 -sl 28,16
```
訓練データ及び，十分の一のサイズのテスト用データと検証用データが生成されます

## data directory structure

```
.
└── data
	└─MNIST-A
	    ├── train_X
	    ├── valid_X
	    ├── test_X
	    ├── train_y.npy
	    ├── valid_y.npy	    	 
	    └── test_y.npy
```

## data loader
data loader用のコードとして，mnist_A_data_loader.pyも用意しました

使い方例
```python
from mnist_A_data_loader import get_mnist_A_loader

train_loader = get_mnist_A_loader("./data/MNIST_A/train_X/",
                                  "./data/MNIST_A/train_y.npy")
test_loader = get_mnist_A_loader("./data/MNIST_A/test_X/", 
                                 "./data/MNIST_A/test_y.npy")
valid_loader = get_mnist_A_loader("./data/MNIST_A/valid_X/", 
                                  "./data/MNIST_A/valid_y.npy")
```

