# paper-reading

# 10.1

##  Exploiting Sentential Context for Neural Machine Translation (Wang et al., arXiv, 2019)

従来の翻訳モデルのdecoderはencoderの最後のhidden vectorsしか使わない。source sentence の単語の意味やlinguistics information などをうまく使うため、本研究ではencoderの全層のhidden vectorを使ってsentence context vector を作り、decoderの全層で使う。

単語のembeddingだけを使うshallow contextと全層を使うdeep contextを提案した。deepの方が良い。encoderの情報を抽出する時RNNとTAM (transparent attention model)を試してどっちでも良さそう。 

##  Assessing the Ability of Self-Attention Networks to Learn Word Order (Yang et al., arXiv, 2019)

RNNと比べてSelf-Attention Networks (SAN)が単語の位置の情報をうまく取れないと言われた。本研究ではSANが単語の順番の情報を保てるかどうかを確認。

文の一つの単語の位置を換わり、換わった単語と元の位置を予測するのがタスク。ゼロからトレーニングしたRNNとSANを比べると確かにRNNの方が精度が高い。しかし、MTのタスクでPre-trainingしたSANのEncoderを使えばSANのほうが精度が高い。

ここでLearning Objectives Matter Moreという結論が出た。SANモデルでも単語位置の情報をうまく取れるということも証明した。



## Extreme Adaptation for Personalized Neural Machine Translation (Michel and **Neubig**, arXiv, 2018)

同じ言語でも人によって癖があるので、従来の翻訳モデルは人の癖 (features)を無視するか、あるいは特定な人のデータでfine-tunningする。しかし、無視すれば翻訳の質へ影響がある。fine-tunningしたらparameter costとoverfittingの問題がある。

本研究では人ごとに固有なbias vectorを与え、出力層のsoftmaxのところへ加え、人の特徴を考慮したモデルを作った。full_biasのモデルではすべての人にvocab sizeのbiasを作り、人と人の関連性を考えていない。fact_biasモデルではr個の特徴dimを考え、speakerを特徴空間へ投影し、biasを計算する。この手法によって人の関連性が考慮され、parameterも大幅に減少した。結果としてはBaselineよりBLEU scoreが0.5 point向上を達成した。

# 10.2

## Findings of the First Shared Task on Machine Translation Robustness (Li et al., arXiv, 2019)

ツイッターなどのデータにはいろんなノイズがあるので、MTにとっては大きな挑戦と言われる。このようなデータを翻訳するタスクがmachine translation robustnessと言う。

本論文ではネット上のデータから作ったMTNTというデータセットを挑戦したsystemsを分析して、最も有効な手法をsummaryした。分析によると、data cleaningはBLEUを5 pointsぐらい向上させた。絵文字などを翻訳しなくて直接にコピーするplaceholdersという方法は1.4 points向上させた。Back-translation (BT)などのdata augmentationは5.8 points。domainやdata type (real or BT) のタグ付けのfine-tuningもすごく役に立つ。Ensemblesはどのsystemにおいてもsingle modelより精度が高い。






