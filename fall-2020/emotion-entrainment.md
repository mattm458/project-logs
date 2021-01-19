# Emotion Entrainment

## Project Log


**Other emotion dataset analysis**

I spent a while working with the switchboard-sentiment corpus but unfortunately was unable to produce anything worthwhile with it yet. I believe this is because of a difference in how each project annotates emotion. When we do it, it is based on our turn divisions, and the annotator is only listening to a single speaker. In switchboard-sentiment, a sentiment annotation can apply to several turns across both speakers. In fact, the average sentiment annotation applies to about 3.3 turns. This makes it difficult to do the same kind of turn-based entrainment measurement we were doing to our corpus: adjacent turns are often covered by the same annotation, even though the paper acknowledges that there could be disagreements among turns within an annotation. Because of this, I believe my current attempts at looking for entrainment in this dataset are not very accurate. Some outstanding questions:

* I feel this comparative analysis would be useful, but is it useful enough to keep investing so much time into?
* Is it worth trying to salvage the switchboard sentiment corpus, or should I try others?
* What other datasets should I look into?

**Continuing work on our emotion dataset**

I did an analysis of session-level proximity in the style of the Levitan and Hirschberg paper and was unable to find a significant difference between a speaker's emotional state and their partner's versus the emotional state of speakers in sessions with whom they did not speak. I am working on an analysis of the difference between the speaker's emotional state and their partner's versus the emotional state of themselves in other conversations.

In terms of next steps, I am considering the following enhancements to the analysis:

* Currently, I am averaging all the emotions supplied by all annotators for a single turn. I should look into whether there are disagreements between annotators - how many and by how much.
* Currently, I am averaging multiple emotions within a turn. I want to repeat the analysis but account for separate emotions, assuming they apply linearly along the turn. There is some justification for this (annotators were instructed to apply emotions in sequence).
* Turns with missing emotions are not a concern and do not need to be automatically annotated. They represent turns with less than a second of speech.


**Papers**

Andreas gave me these:

Youssef, A. Ben, Chollet, M., Jones, H., Sabouret, N., Pelachaud, C., & Ochs, M. (2015). Towards a Socially Adaptive Virtual Agent. International Conference on Intelligent Virtual Agents, 3–16. https://doi.org/10.1007/978-3-540-85483-8

Acosta, J. C., & Ward, N. G. (2011). Achieving rapport with turn-by-turn, user-responsive emotional coloring. Speech Communication, 53(9), 1137–1148. https://doi.org/10.1016/j.specom.2010.11.006

An updated table with all results is shown below:


---

My next steps are:
* Finish the remaining missing entrainment measures (there were some technical hurdles on global proximity and synchrony).
* Investigate whether emotion prediction techniques can be used to fill in missing emotion data for analysis, in the same way that dialogue act prediction techniques added more data for analysis in that other paper. 
* Entrainment analysis on discrete emotion annotation values. There are the older emotion annotations (before V/A) and that Switchboard dataset with more general positive/negative sentiments. How similar would that be, and is that useful?

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