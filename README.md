# SCDVを使って、文書分散表現を獲得


## SCDV概要

SCDV: Sparse Composite Document Vectors using soft clustering over distributional representations

SCDVは、簡単に言えば、

__単語をベクトル化（分散表現）にして、ソフトクラスタリング__ するという手法。

数値実験では、LDA, doc2vecといった既存のアルゴリズムより精度が良い

元論文はこちら <https://arxiv.org/pdf/1612.06778.pdf>

## SCDV アルゴリズム

SCDVのアルゴリズムは、以下の通り。


<img width="341" alt="スクリーンショット 2022-09-29 18 38 09" src="https://user-images.githubusercontent.com/112540428/192997545-e492ba23-9291-4207-8b8f-4efefe9c2eb8.png">

アルゴリズムそのものは、単純。

1. 単語のベクトル $w_{i}$ を取得 （word2vec など）
2. ある単語 $w_{i}$ のIDF値 $idf(w_{i})$ を計算
3. GMM（ガウス混合モデル）を用いて、単語ベクトルのクラスリングを行い、各単語ベクトルが各クラスタに所属する確率 $P(c_{k}|w_{i})$ を取得
4. クラスタを考慮した単語ベクトル、 $wcv_{ik} = wv_{i} \times P(c_{k}| w_{i})$ を算出
5. idf値を考慮した単語ベクトル、 $wtv_{i} = idf(w_{i}) \times \oplus_k^K$ を算出
6. ドキュメント $D_{n} についてベクトルを初期化
7. スパース化（0に近いものは、全部0に押しつぶす）

