# Emotion Entrainment Log

## Highlights for this week
* Revisited old code, revised to make it more similar to the final B-MIC analysis code.
* Evaluated summary synchrony and local proximity on acoustic-prosodic features separately for positive and negative V/A

Starting a new log because the last one got overloaded with general entrainment work on B-MIC.

Some improvements since last time:
* General emotion entrainment measures are computed using speaker-normalized valence and arousal, computed over all V/A values from all annotators across all sessions for a single speaker.
* Turn-level emotion entrainmet is computed by comparing the mean of each of the 3 adjacent emotion annotations. If all 3 annotators left 1 annotation for a whole turn, then it is simply the mean of those 3 annotations. However, if an annotator left more than one emotion annotation, only the first/last annotation as appropriate is incorporated into the mean. This didn't make a huge difference in practice.
* Overlapping turns are skipped as they were in the original B-MIC analysis.

## Emotion/AP Distance Correlates
This section examines the difference between emotions and acoustic-prosodic features across turn exchanges. At turn exchanges where there is both an emotion annotation and a/p annotation for both speakers, we compute the difference of the emotion annotation and the difference of the a/p feature and compare them with Pearsons's correlation coefficient.

### Games
For game sessions, the difference in arousal is positively correlated with the difference in mean and max intensity, mean pitch, NHR, and speaking rate. The difference in valence is only positively correlated with a difference in max pitch.
|                | Valence r             | p                   | dof | Arousal r              | p                      |
|----------------|-----------------------|---------------------|-----|------------------------|------------------------|
| Mean intensity | -0.008063929987601543 | 0.8101473338583689  | 889 | 0.2967219569572294     | **1.5092739144479908e-19** |
| Max intensity  | -0.00900836135001011  | 0.788412217989601   | 889 | 0.2737820782753171     | **9.12746828814226e-17**   |
| Mean pitch     | 0.08715281692638693   | **0.00928670057727018** | 889 | 0.06750662849393714    | **0.04407434737947286**    |
| Max pitch      | 0.027720094933604816  | 0.40882314052579516 | 889 | -0.0397720654667957    | 0.23589243561240097    |
| Jitter         | 0.01154519617893882   | 0.730881093678039   | 889 | 0.05411359598276809    | 0.10668432458930513    |
| Shimmer        | 0.006401052194624063  | 0.8487643061586664  | 889 | -0.0017198304047841837 | 0.9591379411329057     |
| NHR            | 0.008737263854195432  | 0.7946352444423297  | 889 | 0.06594759059915516    | **0.04920833723355125**    |
| Rate           | 0.045180750096295706  | 0.17808822918116893 | 889 | 0.09975770328294557    | **0.002888979917956301**   |

### Conversations
There is no correlation between emotion difference and A/P differences at turn exchanges except for arousal and mean intensity (r=0.12351237225358844, p=0.03853251074475086, dof=280)

## Extreme emotion value entrainment
In this section, we examine the effect a speaker's emotional state has on his or her partner's entrainment behavior. We examine the emotion values in the first turn at turn exchanges, filtering out turn exchanges where the value does not pass a threshold value. The partner's emotional state is not considered.

### Similarity
#### Games
|                | Valenece >= 0 t | p      | dof  | Valence < 0 r | p     | dof |   | Arousal >= 0 t | p      | dof  | Arousal < 0 r | p       | dof |
|----------------|-----------------|--------|------|---------------|-------|-----|---|----------------|--------|------|---------------|---------|-----|
| Intensity mean |                 | NS     |      |               | NS    |     |   | -3.32          | 0.0009 | 1164 | 4.09          | 4.73e-5 | 835 |
| Intensity max  | -3.43           | 0.0006 | 1005 |               | NS    |     |   | -5.10          | 3.91   | 1164 |               | NS      |     |
| Pitch mean     |                 | NS     |      |               | NS    |     |   |                | NS     |      |               | NS      |     |
| Pitch max      |                 | NS     |      |               | NS    |     |   |                | NS     |      |               | NS      |     |
| Jitter         | -2.05           | 0.04   | 912  |               | NS    |     |   |                | NS     |      | -2.043        | 0.041   | 777 |
| Shimmer        |                 | NS     |      |               | NS    |     |   |                | NS     |      |               | NS      |     |
| NHR            |                 | NS     |      |               | NS    |     |   |                | NS     |      |               | NS      |     |
| Rate           |                 | NS     |      |        2.38   | 0.018 | 994 |   | 2.76           | 0.0059 | 1164 |               | NS      |     |

#### Conversations
|                | Valenece >= 0 t | p     | dof | Valence < 0 r | p       | dof |   | Arousal >= 0 t | p      | dof | Arousal < 0 r | p     | dof |
|----------------|-----------------|-------|-----|---------------|---------|-----|---|----------------|--------|-----|---------------|-------|-----|
| Intensity mean |                 | NS    |     |               | NS      |     |   |                | NS     |     |               | NS    |     |
| Intensity max  | -2.07           | 0.039 | 338 | -3.49         | 0.00057 | 278 |   | -3.11          | 0.0020 | 310 | -2.54         | 0.012 | 306 |
| Pitch mean     |                 | NS    |     |               | NS      |     |   | 2.44           | 0.015  | 308 |               | NS    |     |
| Pitch max      |                 | NS    |     | 2.02          | 0.044   | 276 |   |                | NS     |     |               | NS    |     |
| Jitter         |                 | NS    |     |               | NS      |     |   |                | NS     |     |               | NS    |     |
| Shimmer        |                 | NS    |     |               | NS      |     |   |                | NS     |     |               | NS    |     |
| NHR            |                 | NS    |     |               | NS      |     |   |                | NS     |     | -2.03         | 0.043 | 305 |
| Rate           | -2.00           | 0.046 | 338 |               | NS      |     |   |                | NS     |     |               | NS    |     |

### Synchrony
#### Games
For games, there doesn't appear to be a major difference in AP entrainment between positive and negative emotion values. Slight entrainment on jitter is present when valence < 0 and arousal >= 0, and there is no evidence for shimmer when arousal > 0. Entrainment on NHS is only present for arousal.

|                | Valenece >= 0 r | p        | dof  | Valence < 0 r | p       | dof |   | Arousal >= 0 r | p       | dof  | Arousal < 0 r | p        | dof |
|----------------|-----------------|----------|------|---------------|---------|-----|---|----------------|---------|------|---------------|----------|-----|
| Intensity mean | 0.19            | 5.42e-10 | 1005 | 0.12          | 0.00028 | 994 |   | .11            | 0.00015 | 1164 | 0.14          | 3.41e-05 | 835 |
| Intensity max  | 0.14            | 5.663-06 | 1005 | 0.09          | 0.0047  | 994 |   | 0.09           | 0.0024  | 1164 | 0.10          | 0.0025   | 835 |
| Pitch mean     |                 | NS       |      |               | NS      |     |   |                | NS      |      |               | NS       |     |
| Pitch max      |                 | NS       |      |               | NS      |     |   |                | NS      |      |               | NS       |     |
| Jitter         |                 | NS       |      | 0.08          | 0.011   | 952 |   | 0.07           | 0.018   | 1087 |               | NS       |     |
| Shimmer        | 0.07            | 0.04     | 903  | 0.07          | 0.042   | 951 |   |                | NS      |      | 0.09          | 0.014    | 772 |
| NHR            |                 | NS       |      |               | NS      |     |   | 0.09           | 0.0037  | 1162 | 0.11          | 0.0015   | 829 |
| Rate           |                 | NS       |      |               | NS      |     |   |                | NS      |      |               | NS       |     |

#### Conversations
Conversations show significant differences between positive and negative emotional values. When valence >= 0, there is evidence for synchrony over intensity max and pitch mean. When arousal >= 0, there is evidence for synchrony over intensity mean and max and mean pitch. There is no evidence for synchrony with negative valence or arousal.

|                | Valenece >= 0 r | p     | dof | Valence < 0 r | p  | dof |   | Arousal >= 0 r | p      | dof | Arousal < 0 r | p  | dof |
|----------------|-----------------|-------|-----|---------------|----|-----|---|----------------|--------|-----|---------------|----|-----|
| Intensity mean |                 | NS    |     |               | NS |     |   | 0.18           | 0.0017 | 310 |               | NS |     |
| Intensity max  | 0.11            | 0.043 | 338 |               | NS |     |   | 0.13           | 0.026  | 310 |               | NS |     |
| Pitch mean     | 0.13            | 0.018 | 337 |               | NS |     |   | 0.16           | 0.0040 | 308 |               | NS |     |
| Pitch max      |                 | NS    |     |               | NS |     |   |                | NS     |     |               | NS |     |
| Jitter         |                 | NS    |     |               | NS |     |   |                | NS     |     |               | NS |     |
| Shimmer        |                 | NS    |     |               | NS |     |   |                | NS     |     |               | NS |     |
| NHR            |                 | NS    |     |               | NS |     |   |                | NS     |     |               | NS |     |
| Rate           |                 | NS    |     |               | NS |     |   |                | NS     |     |               | NS |     |

## Global Emotion Entrainment

### Proximity

#### Partner vs. other distance
For valence, partners are significantly more similar to one another than to others in games (t=3.8464652335977143, p=0.00035984515799359436, dof=47) and conversations (t=2.0910731874299846, p=0.04481099918776943, dof=31). There is no significant difference between partners and others for arousal.

#### Partner vs self distance
For valence, partners are significantly more similar to one another than to themselves in games (t=3.62211689045235, p=0.0007145391979325383, dof=47) and conversations (t=2.973186033431553, p=0.0056599846403571335). For arousal, partners are more similar to one another only in games (t=2.016626883693224, p=0.04946831753014236, dof=47)

### Convergence
There is only weakly significant global divergence in arousal for games. t=-2.623045586392091, p=0.015203616417768481, dof=23.

## Local Emotion Entrainment

### Proximity
At turn exchanges, speakers are more similar to their partner at turn exchanges than they are to their partner at other random turns in the session for every measure except arousal in conversations.

|              | Valence                                                | Arousal                                                |
|--------------|--------------------------------------------------------|--------------------------------------------------------|
| Game         | t=5.299422498246197, **p=1.4603307540982257e-07**, dof=904 | t=4.887760461701219, p=**1.2064070558496025e-06**, dof=904 |
| Conversation | t=3.742898870335481, **p=0.00022000883786183595**, dof=285 | t=0.3533072628555414, p=0.7241192910753673, dof=285    |

### Convergence
When viewed in summary, convergence does not occur except a small divergence in game sessions (r = -0.11489340497616259, p = 0.0005340688510017756 dof = 904).

| # Game | valence r          | valence p             | valence dof | arousal r          | arousal p             | arousal dof | # Conv | valence r          | valence p             | valence dof | arousal r          | arousal p             | arousal dof |
|--------|--------------------|-----------------------|-------------|--------------------|-----------------------|-------------|--------|--------------------|-----------------------|-------------|--------------------|-----------------------|-------------|
| 1      | -0.48298654674511  | **0.009230068100982** | 27          | -0.224132588491783 | 0.251552321617664     | 27          |        |                    |                       |             |                    |                       |             |
| 2      | -0.289387432601789 | 0.120879827433481     | 29          | -0.097847703031388 | 0.606973418366247     | 29          |        |                    |                       |             |                    |                       |             |
| 3      | -0.23041043528125  | 0.229177367231746     | 28          | -0.135398577890785 | 0.483736273922137     | 28          | 11     | -0.245578325862032 | 0.207803316560256     | 27          | -0.236751772885114 | 0.225132504901716     | 27          |
| 4      | -0.269505748402117 | 0.192641965417455     | 24          | -0.026552403225386 | 0.899742269448427     | 24          | 12     | 0.42789055953933   | 0.126943236588855     | 13          | -0.379723942605323 | 0.180521664519935     | 13          |
| 5      | 0.106913450524941  | 0.517106549402064     | 38          | -0.226305132788364 | 0.165947767606218     | 38          | 13     | 0.24195179516601   | 0.233718186827718     | 25          | -0.230031168959948 | 0.258269988616336     | 25          |
| 6      | -0.126879145059516 | 0.545599189331315     | 24          | 0.303389392794623  | 0.140402949091512     | 24          | 14     | -0.173314616614563 | 0.452467320760046     | 20          | -0.389306708599834 | 0.081095424124772 (!) | 20          |
| 19     | -0.307921369444501 | 0.076453313564354     | 33          | 0.083116768384124  | 0.640262386511707     | 33          |        |                    |                       |             |                    |                       |             |
| 20     | -0.02465373448536  | 0.863654440392866     | 50          | -0.285531046837084 | **0.042250364048299** | 50          |        |                    |                       |             |                    |                       |             |
| 21     | 0.136481322484479  | 0.413896228387652     | 37          | -0.207533847383947 | 0.211206715525997     | 37          | 15     | 0.485962640047819  | **0.021846449820819** | 21          | 0.0651284784391    | 0.773382096485497     | 21          |
| 22     | -0.21209208011785  | 0.343347177426761     | 21          | -0.219594331786294 | 0.326138780914244     | 21          | 16     | 0.348662989978307  | 0.221803377564085     | 13          | 0.536547988892712  | **0.047917935160766** | 13          |
| 23     | 0.040842410776887  | 0.794834361927331     | 42          | -0.073435065828551 | 0.639792509715179     | 42          | 17     | 0.067451849840034  | 0.84378871176441      | 10          | 0.108511215329916  | 0.750803148715015     | 10          |
| 24     | -0.035148502681809 | 0.848542744723566     | 31          | 0.331019748197622  | 0.064228481678109     | 31          | 18     | 0.505940650944763  | 0.093301877136229     | 11          | 0.031508960380815  | 0.922560972023603     | 11          |
| 29     | -0.114817011961799 | 0.629795876818059     | 19          | -0.183333002994    | 0.43911390884934      | 19          |        |                    |                       |             |                    |                       |             |
| 30     | -0.191046188501885 | 0.271610448537459     | 34          | -0.132162413520757 | 0.449159776246277     | 34          |        |                    |                       |             |                    |                       |             |
| 31     | 0.388420300726319  | 0.060696693539972     | 23          | -0.441467375085676 | **0.030801409951655** | 23          | 39     | -0.191468490842248 | 0.596182534604958     | 9           | -0.708256561700202 | **0.021891042178953** | 9           |
| 32     | -0.294457040532065 | 0.121008315221725     | 28          | -0.302383293425421 | 0.110860726629395     | 28          | 40     | 0.489308170208411  | **0.008227721138623** | 27          | 0.246714418973245  | 0.205640901435747     | 27          |
| 33     | -0.130002780558835 | 0.493525135629652     | 29          | -0.355902640653201 | 0.053573990272341     | 29          | 41     | -0.084097360726468 | 0.709828155123769     | 21          | -0.585945535245738 | **0.004163066134896** | 21          |
| 34     | 0.180650552130479  | 0.421098012071282     | 21          | -0.254247556836477 | 0.253535650876058     | 21          | 42     | 0.096711838718771  | 0.711943168230615     | 16          | -0.043148656304809 | 0.869391932963836     | 16          |
| 47     | 0.34381589923231   | **0.012573800210225** | 51          | -0.103855980232059 | 0.463744148051454     | 51          |        |                    |                       |             |                    |                       |             |
| 48     | -0.069748093179016 | 0.549371452108428     | 75          | -0.231877846390591 | **0.04384993883687**  | 75          |        |                    |                       |             |                    |                       |             |
| 49     | 0.048716202734137  | 0.706910444363546     | 61          | 0.206364047554435  | 0.107568799419628     | 61          | 43     | -0.235446328987573 | 0.202290270442068     | 30          | -0.173085190232248 | 0.351776219879256     | 30          |
| 50     | 0.190158809854415  | 0.216318572097599     | 43          | -0.005611270695186 | 0.971163009845178 (!) | 43          | 44     | -0.305145645545873 | 0.462376400921774     | 7           | 0.345257618059804  | 0.402246866901121     | 7           |
| 51     | 0.009653630173963  | 0.94981618158777 (!)  | 44          | 0.015446516186166  | 0.919781889024809     | 44          | 45     | 0.088427142365805  | 0.835061385092202 (!) | 7           | 0.320707082837106  | 0.438634085305154     | 7           |
| 52     | -0.00995139555603  | 0.93483581101886      | 69          | -0.257912165286795 | **0.031114352263633** | 69          | 46     | 0.106561944370844  | 0.716919138103609     | 13          | -0.28531552949476  | 0.322771711612608     | 13          |

### Synchrony
I found synchrony is best viewed in summary, as it shows a pretty clear general trend. We get some nice graphs out of it, which is a little more intuitive to look at than just charts.

|              | Valence                                                                                | Arousal                                                                                 |
|--------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Game         | r = 0.29581054778739274, **p = 9.82658694514841e-20**   ![](img/synchrony-valence-game.png) | r = 0.20432425029451187, **p = 5.511657581692854e-10**   ![](img/synchrony-arousal-game.png) |
| Conversation | r = 0.3190451967191962, **p = 3.453148612728739e-08**   ![](img/synchrony-valence-conv.png) | r = 0.0812930720714577, p = 0.1703624963432945   ![](img/synchrony-arousal-conv.png)     |