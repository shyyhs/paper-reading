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

ツイッターなどのデータには様々なノイズがあるので、MTにとっては大きな挑戦だといわれている。このようなデータを翻訳するタスクをmachine translation robustnessと言う。

本論文ではネット上のデータから作ったMTNTというデータセットに取り組んだsystemsを分析して、最も有効な手法をsummaryした。分析によると、data cleaningはBLEUを5 points程度向上させた。絵文字などを翻訳せず直接コピーするplaceholdersという方法は1.4 points向上させた。Back-translation (BT)などのdata augmentationは5.8 points。domainやdata type (real or BT) のタグ付けのfine-tuningも非常に有効。Ensemblesはどのsystemにおいてもsingle modelより精度が高い。

## Toward Robust Neural Machine Translation for Noisy Input Sequences (Sperber et al., IWSLT, 2017)

話し言葉の翻訳はノイズがあるので、書き言葉よりNMTのロバスト性が期待されている。本研究ではトレーニングデータセットに適量のノイズを加えて、システムのロバスト性を向上させた。

具体的にノイズが三種類ある：substitution, insertion, deletion。いずれも単純な手法だが、ノイズの量をうまくコントロールすれば翻訳の質の向上が達成できる。三種類のノイズの比例と量について様々な実験をした。トレーニングデータに加えたノイズがテストデータのノイズより少ないほうがいいという結論ができた。

## An Empirical Comparison of Domain Adaption Methods for Neural Machine Translation (Chu, Dabre and Kurohashi, ACL, 2017)

データが少ないdomainにおいて、fine-tuningがよく使われている。まず大量のout-of-domainのデータでトレーニングし、最後の数千stepsはin-domainデータのみに訓練。手間かかずにモデル自体も変わらないので様々なシチュエーションでよく使われている。従来の問題としてはin-domainのデータが少ないのでoverfittingの問題は非常に深刻である。

本研究ではfine-tuningの時にin-domainのデータのみならずin-domainとout-of-domainのデータをミックスしてfine-tuningする。方法は単純だがover-fittingを確実に避けた。さらに、従来はin-domainデータしか処理できないが、今のモデルはin-domainとout-of-domain両方処理できる。 

# 10.3

## Exploiting Out-of-Domain Parallel Data through Multilingual Transfer Learning for Low-Resource Neural Machine Translation (Imankulova et al., arXiv, 2019)

特定のdomainの低資源言語ペアをうまく翻訳するため、本研究ではmultistage fine-tuningという方法を提出した。実験によるとIn-domainデータだけて翻訳がうまくできないが、低資源言語ペアにはout-of-domainのデータもない。高資源ペアのデータとIn-domainのデータを使うため以下の仕組みを提出した。

１、Out-of-domainかつ高資源言語ペアのデータでモデルをpre-trainingする。２、すべての言語ペアのIn-domainデータでfine-tuningする。３、目標言語ペアかつIn-domainデータのみでfine-tuningする。すべてのデータを使っているので、実験によるとmultistage fine-tuningの方がone stageよるBLEUが高い。 


# 10.4

## Exploring Transfer Learning and Domain Data Selection for the Bio-medical translation (Hira et al., WMT, 2019)

Bio-medicalのparallelデータが少ない一方、newsなどのデータがすごく多い。本研究ではnewsなどのdomainからbio-medical domainをtransfer learningの手法をデザインした。

Bio-medicalのデータセットを利用し、文ごとに大規模なout-of-domainデータセットからtop nの似ている文を探して新たなin-domainデータセットを作った。Out-of-domainデータセットでトレーニングしたモデルを作ったデータセットとin-domainのデータセットでfine-tuningしてbaselineより +7.5 BLEU score達成した。

## Target Conditioned Sampling: Optimizing Data Selection for Multilingual Neural Machine Translation (Wang and Neubig, ACL, 2019)

テストdomainと似ているfine-tuningのためのデータを選択する、言語ペア間と文ペア間のsimilarityの定義を提案した。まず、トレーニングの時テストdomainとのsimilarityが高いデータを選択する方がいいTarget Conditioned Samplingという理論を提出して。

言語ペアと文ペアのsimilarityを測る方法が２つ提案された。１つ目は言語の辞書のoverlap。文の場合は文の単語のoverlap。２つ目はある言語でトレーニングしたLanguage Modelを使って、他の言語の文がこのモデルでの確率を測り、similarityとして使う。

## H2@BUCC18: Parallel Sentence Extraction from Comparable Corpora Using Multilingual Sentence Embeddings (Bouamor and Sajjad, BUCC, 2019)

# 10.7

## Distilling the knowledge in a neural network (Hinton et al., arXiv, 2015)

## Sequence-Level Knowledge Distillation (Kim and Rush, EMNLP, 2016)

# 10.8

## Chinese-Portuguese Machine Translation: A Study on Building Parallel Corpora from Comparable Texts (Liu et al., arXiv, 2018)

## Bridging the Gap between Training and Inference for Neural Machine Translation (Zhang et al., ACL, 2019)

# 10.10

## Search Engine Guided Neural Machine Translation (Gu et al., AAAI, 2018)

## Transductive Data-Selection Algorithms for Fine-Tuning Neural Machine Translation (Poncelas et al., PSLT, 2019)

## One Sentence One Model for Neural Machine Translation (Li et al., arXiv, 2016)

## To Tune or Not to Tune? Adapting Pretrained Representations to Diverse Tasks (Peters et al., RepL4NLP, 2019)

# 10.11

## Memory-based Parameter Adaptation (Sprechmann et al., ICLR, 2018)

# 10.15

## A Japanese-English patent parallel corpus (Utiyama and Isahara, Proceedings of MT summit XI, 2007)

# 10.17

## Improving Transformer-based Speech Recognition Systems with Compressed Structure and Speech Attributes Augmentation (Li et al., INTERSPEECH, 2019)


