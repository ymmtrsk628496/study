# ESG Confusion and Stock Returns: Tackling the Problem of Noise

## 3 ESG Discrepancies and Expected Stock Returns

- データについて
- 株式リターンに関連するESG評価におけるシグナルとノイズを分離する操作変数法（IV法）について

### 3.1 Data

- ESGデータについて
  - データ対象期間は2014から2020（Sustainalyticsデータが2014からだから）
  - スコアが高いほうがESGパフォーマンスがいい（RepRisk, Sustainalyticsはリスクを測っているのでスコアの符号を反転している）
  - 対象期間に評価方法を変更したものがある
    - Sustainalytics: 201812にメソドロジーを変更
    - MSCI: 2017にメソドロジーを更新
  - 評価機関が過去データのスコアを変更した可能性がある
    - Refinitive ([Berg, Fabisik and Sautner, 2021](https://ecgi.global/sites/default/files/working_papers/documents/bergfabisiksautnerfinal.pdf))
    - Sustainalytics: 新メソドロジーに基づき2018以前のスコアを独自に提供

- モチベ
  - non-point-in-time dataにはlook-aheadバイアスが含まれているが，この問題を対処していく．

- 金融データについて
  - Thomson Reuters Worldscope
  - 月次データ
    - リターン
    - PBR
    - ベータ
    - 総資産
    - BEP ratio (ebit-over-total-assets ratio)
    - size
  - 月次リターンデータを用いて12Mモメンタムと12Mボラティリティを算出

- ESGスコア間相関
  - -0.57 (Refinitive vs RepRisk in Europe) - 0.71(Viego-Eiris vs Refinitive in Japan)
  - RepRiskスコアは他の多くのスコアと負の相関
  - 3地域間（北アメリカ，ヨーロッパ，日本）で相関は似ている

#### 3.1.1 ESG Ratings Methodologies and Data Sources

ESG ratingは観測不可能な「真の」ESGパフォーマンスのノイズの多い測定値

- materiality, methodology, etcが違う
- データソースの種類が様々

### 3.2 Errors-in-Variables and Stock Returns

主題
- ESG測定誤差が与えるESGパフォーマンスとストックリターンの関係

前提
- ESG属性がratingsによって正確に測定されると仮定しない

方程式

$$
E \left( S_1 \right) - S_0 = c_0 - c_{impact} \cdot c_{noise} \cdot \left( s_Y - \bar{Y} \right) + c_X \cdot X + \eta \tag{14}
$$
- $X \in \mathbb{R}^n$: 観測可能なキャッシュフローに関連する企業の特性（制御変数，control）
- シグナルにノイズがない中でESG格付けが向上することで，どの程度ストックリターンに影響を与えるか：
$$
c_{impact} = A \lambda \frac{\sigma_D^2 \sigma_{\epsilon_D}^2}{\sigma_D^2 + \sigma_{\epsilon_D}^2}
$$
- ノイズにより低減するインパクト：
$$
c_{noise} = \frac{\sigma_{Y}^2}{\sigma_Y^2 + \sigma_{\epsilon_Y}^2} < 1
$$
-$\eta$: 観測可能な企業特性$X$を制御した後の企業キャッシュフローシグナル$s_d$に依存する項に対応
-$c_0$: 式(13)の定数
- The noise-to-signal ratio in the ESG signal
$$
\kappa = \frac{\sigma_{\epsilon_Y}^2}{\sigma_{Y}^2}
$$

```Because of the noise in the signal, it will produce an estimate that is biased towards zero. This is a manifestation of the “attenuation bias,” arising in the context of the errors-in-variables problem.```

