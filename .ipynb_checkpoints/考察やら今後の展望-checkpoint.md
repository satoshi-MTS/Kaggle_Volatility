# 理解したカーネル

- Intoroduction to financial conxepts and data(Most Vote1)   
    導入（公式）
- LightGBm starter with feature engineering iead(Most Vote2)  
    LGBMを使用したカーネル
- Optiver Realized Volatility LGBM Baseline(Mosr Vote3)  
    上のカーネルの進化系（上でやってることは全部やってる。）
    



# Public Scoreについて

見ての通りもらえてるtest_dataはあってないようなものになるので、スコアの参照にはあまり役立たない....  
解決策としては  
- CVでの評価
    実際のPBがどんなデータなのかわからないのでどれくらいの差があるかは試してみないとわからない  
    結局あてにならないかもしれないけど、提出回数が決まっているので足切りラインには使えるかも
    
- LBでの検証  
    最も効率的ではあるが、提出に時間がかかる。また、どんなデータで検証しているのか全くわからない...  
    欠損具合がわからないので、統計指標を使っている
    
そもそも、PBがLBにどれくらい関係するかと言われてもわからないのであくまで参考値程度になってしまう。  
明確なスコアがないのでこれは....


# stock_id, time_id毎の統計指標

Optiver Realized Volatility LGBM Baselineで使われた統計指標 
stock_id毎の統計指標ってtime_idの値を見ないから、未来の情報を含むよね...  
リーク問題があるが、kaggleに限った話ならつかっておkっていうのが一般的っぽい？  

今回の評価方法ってコンペ終了後の3ヶ月のデータを収集して、その間のボラティリティを計算するのか  
はたまた、未来の予測にするのかによって大きく変わる  
未来予測になるのであれば、ターゲットエンコーディング自体使えないしとういった統計予測もできない

# score

LightGBm starter with feature engineering iead  
- cv : 0.2344
- LB : 0.22009(自分はだしてない) 

Optiver Realized Volatility LGBM Baseline(no leak)
- cv : 0.2294
- LB : 0.22(自分はだしてない)
- 特徴量としてはwap2をふやしているだけ  
- あとは統計的な指標と、秒数を150.450を増やしている  
- それだけでcv0.005スコア変動


Optiver Realized Volatility LGBM Baseline(leak?)  
- cv : 0.2018
- LB : 0.212(自分出してない)
- stock_id, time_idの統計指標を使用している。  
- cv0.027の効果がでている

# 特徴量選択について

train, valで　アーリーストップでやった場合、それでスコアが上がっても未知のデータに対しては落ちる可能性がある。  
(valに対してはたまたまノイズか何かで傾向が見られてスコアが上がっているイメージ) 　
解決するには全く未知のデータを用意してあげて、それに対してのスコアを見る以外の方法はわからん...  
kaggleであれば提出してスコア見るっていうやり方ができるけど時間がくっそかかる



# ボラティリティ

# LGBM パラメータについて

現在は特に考えていない  
ぎりぎりになったら始める

# アンサンブルについて

まだ

# 特徴量組み合わせについて

まだ