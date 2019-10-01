# paper-reading

# 10.1

##  Exploiting Sentential Context for Neural Machine Translation (Wang et al., arXiv, 2019)

従来の翻訳モデルのdecoderはencoderの最後のhidden vectorsしか使わない。source sentence の単語の意味やlinguistics information などをうまく使うため、本研究ではencoderの全層のhidden vectorを使ってsentence context vector を作り、decoderの全層で使う。

単語のembeddingだけを使うshallow contextと全層を使うdeep contextを提案した。deepの方が良い。encoderの情報を抽出する時RNNとTAM (transparent attention model)を試してどっちでも良さそう。 

##  Assessing the Ability of Self-Attention Networks to Learn Word Order (Yang et al., arXiv, 2019)

RNNと比べてSelf-Attention Networks (SAN)が単語の位置の情報をうまく取れないと言われた。本研究ではSANが単語の順番の情報を保てるかどうかを確認。

文の一つの単語の位置を換わり、換わった単語と元の位置を予測するのがタスク。ゼロからトレーニングしたRNNとSANを比べると確かにRNNの方が精度が高い。しかし、MTのタスクでPre-trainingしたSANのEncoderを使えばSANのほうが精度が高い。

ここでLearning Objectives Matter Moreという結論が出た。SANモデルでも単語位置の情報をうまく取れるということも証明した。



