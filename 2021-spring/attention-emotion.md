# Emotion prediction with attention networks

## 2021/4/20

I've been implementing a hierarchical attention network modeled after this paper: https://www.cs.cmu.edu/~./hovy/papers/16HLT-hierarchical-attention-networks.pdf

It's trying to do a binary classification of either valence or arousal, and it will do it either from words alone or from acoustic-prosodic features. The attention network is capable of focusing on individual words and individual features, if available.

Right now it is having difficulty converging, and I'm not sure if the network is too complex for the amount of data we have available (this is very possible) or if it's just a difficult task.

Valence with A/P features:

```
              precision    recall  f1-score   support

           0       0.55      0.16      0.25       158
           1       0.68      0.93      0.78       296

    accuracy                           0.66       454
   macro avg       0.61      0.55      0.52       454
weighted avg       0.63      0.66      0.60       454
```

Valence without A/P features:

```
              precision    recall  f1-score   support

           0       0.51      0.16      0.24       158
           1       0.67      0.92      0.78       296

    accuracy                           0.65       454
   macro avg       0.59      0.54      0.51       454
weighted avg       0.62      0.65      0.59       454
```


Arousal with A/P features:

```
              precision    recall  f1-score   support

           0       0.57      0.21      0.31        75
           1       0.86      0.97      0.91       379

    accuracy                           0.84       454
   macro avg       0.72      0.59      0.61       454
weighted avg       0.81      0.84      0.81       454
```

Arousal without A/P features:

```
              precision    recall  f1-score   support

           0       0.00      0.00      0.00        75
           1       0.83      1.00      0.91       379

    accuracy                           0.83       454
   macro avg       0.42      0.50      0.45       454
weighted avg       0.70      0.83      0.76       454
```