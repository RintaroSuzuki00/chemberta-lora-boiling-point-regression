# ChemBERTa + LoRA による沸点（Tb）回帰予測

分子のSMILES表記から沸点（Tb）を予測する回帰モデルの学習・評価コードです。

## 概要

化学特化BERTモデルである **ChemBERTa-100M-MLM** を、**LoRA（Low-Rank Adaptation）** を用いてパラメータ効率よくファインチューニングし、SMILES文字列から沸点を回帰予測します。

## 使用技術

| カテゴリ | ライブラリ・モデル |
|---|---|
| 事前学習モデル | `DeepChem/ChemBERTa-100M-MLM` |
| ファインチューニング手法 | LoRA（PEFT, r=16, lora_alpha=32） |
| 分子処理 | RDKit（SMILES検証） |
| 学習フレームワーク | Hugging Face Transformers, PyTorch |
| 評価指標 | MSE, RMSE, MAE, R² |

## パイプライン

1. **データ前処理**: RDKitでSMILESの有効性を検証し、無効なサンプルを除去
2. **データ分割**: 訓練 / 検証 / テストセットに分割（StandardScalerで正規化）
3. **モデル構築**: ChemBERTaにLoRAアダプタを適用（学習可能パラメータを削減）
4. **学習**: EarlyStoppingを用いた回帰学習（評価指標: eval_mse）
5. **評価・可視化**: テストセットでの予測精度を評価し、散布図（True vs Pred）を出力

## 実行環境

Google Colab（GPU: T4）上で実行。

## ファイル構成

```
.
└── chemberta_lora_boiling_point_regression.ipynb   # 学習・評価ノートブック
```
