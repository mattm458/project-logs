# Emotion Entrainment

## Project Log

My next steps are:
* Finish the remaining missing entrainment measures (there were some technical hurdles on global proximity and synchrony).
* Investigate whether emotion prediction techniques can be used to fill in missing emotion data for analysis, in the same way that dialogue act prediction techniques added more data for analysis in that other paper. 

---

Here are a set of results from some analysis of extracted emotions based on the various measures of entrainment described in "Measuring acoustic-prosodic entrainment with respect to multiple levels and dimensions".

To get these, I applied the same methodology as described in the paper against valence and arousal separately, as though they were extracted audio features. Additionally, I compared valence and arousal together using Euclidean distance.

Currently, emotion appears to have no global or turn-level convergence (with some exceptions). The most significant forms of entrainment witnessed so far are in turn-level proximity and synchrony. In particular, there appears to be entrainment on the proximity and synchrony of valence, but not arousal.

|                        | V (All)     | A (All) | Distance (All) | V (Game)    | A (Game) | Distance (Game) | V (Conv)    | A (Conv) | Distance (Conv) |
|------------------------|-------------|---------|----------------|-------------|----------|-----------------|-------------|----------|-----------------|
| Global convergence     | 0.41588     | 0.54050 | 0.33413        | 0.26157     | 0.44617  | 0.23013         | 0.87897     | 0.96349  | 0.85888         |
| Turn-level convergence | 0.16226     | 0.12985 |**0.02905**        | **0.02515**     | 0.22459  | **0.01701**         | 0.43663     | 0.33926  | 0.70134         |
| Turn-level proximity   | **2.61404e-09** | 0.06698 | **2.98951e-07**    | **1.68708e-06** | 0.05899  |**1.77216e-05**     | **0.00013**    | 0.62796  | **0.00323**         |
| Turn-level synchrony   | **1.41091e-18** | 0.25623 |                | **9.55685e-11** | 0.13923  |                 | **3.53121e-08** | 0.54941  |                 |

---

I am now pulling emotion information from the Psiturk database. Here are some decisions I made regarding how to process the data:

* If a single turn annotation contains more than one emotion, they are averaged together.
* If a later row describes an annotation for an earlier row which already annotated the same turn, the newer annotation replaces the old.
* If multiple annotators left emotion annotations for the same turn, each annotation is averaged together.
* Earlier rows containing discrete emotional states rather than V/A vectors are ignored.