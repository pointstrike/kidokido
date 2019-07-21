# kidokido
python、opencvでウェブカメラの映像の輝度を分析し、リアルタイムでグラフ表示するプログラムです

### python
import cv2 

import matplotlib.pyplot as plt

#グラフ別ウィンドウ表示

%matplotlib 



#ビデオオブジェクトの宣言

cam = cv2.VideoCapture(0) 

#各変数の初期化

i = 0 

j = 0

x = []

y = []

plt.ion()





while True:

    #動画の画像読み込み

    _, img = cam.read()

    #グレースケールへの変換

    img2 = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)



    cv2.imshow('PUSH ENTER KEY', img) 

    

 

    i= i+1

    j = img2.mean()

    x.append(i)

    y.append(j)

    

    plt.plot(x,y,color='blue')

    plt.title('SimpleGraph') 

    plt.xlabel('times')

    plt.ylabel('brightness')

    plt.ylim(0,255)

    plt.grid()

    plt.draw()

    plt.pause(0.033)



    #Enterで終了

    if cv2.waitKey(1) == 13: break

        

plt.close()

cam.release()



cv2.destroyAllWindows()







### 実装した処理
・リアルタイムグラフ

  　→カメラの映像とグラフを対応させるために、plt.pauseを用いて逐次更新
   
・映像の毎フレーム分析

　　→動画をフレーム単位(今回は30fps)で捉えて、1枚ずつ計算を行った。
  
・グレースケール変換

  　→各ドットのグレースケール→平均値という形で輝度を求めるのにつかった。
   
・カメラウィンドウと、グラフウィンドウの独立

    →Jupiter Notebokk上ではグラフが見づらかったので修正。
    
### 使い方，実行の仕方，依存ライブラリとバージョン 
実行の仕方：

　pythonの環境構築、cmdから必要なopencv関連のインポートを行う。その後、各環境から起動する。※ただし、終了時は映像ウィンドウと、エンターキーを連打しなければならないので注意。


### 使い方：

　カメラを起動して適当に動かせば、自動的にリアルタイムで映像の輝度を更新します。

### 参考にしたサイトなどへのリンク
 
 - https://teratail.com/questions/79656
 - https://news.mynavi.jp/article/zeropython-35/
 - https://qiita.com/airtanker/items/97960dccfb3f2af57dc0 
 - https://qiita.com/hausen6/items/b1b54f7325745ae43e47
 - https://qiita.com/yoya/items/96c36b069e74398796f3

### 参考部分
1. グラフの別ウィンドウ化
- ブラウザ上でプログラムを実行すると、変化するグラフが非常に見づらかったのでウィンドウ表示にした。
- https://teratail.com/questions/79656 の、%matplotlib　を追加する部分を参考にした。

2. カメラの起動と、ウィンドウ表示、終了
- https://news.mynavi.jp/article/zeropython-35/ の一番上のプログラムを参考にした。
3. opencvのインポート
- https://qiita.com/airtanker/items/97960dccfb3f2af57dc0 を環境構築の確認の参考にした。
4. グラフのリアルタイム描画
- https://qiita.com/hausen6/items/b1b54f7325745ae43e47 の中で、plt.pause関連を参考にした。
5. 画像のグレースケール変換
- https://qiita.com/yoya/items/96c36b069e74398796f3 の一番上のプログラムを参考にした。

gifアニメーションは別に添付する
