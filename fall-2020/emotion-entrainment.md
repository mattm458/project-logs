# Emotion Entrainment

## Project Log

### Lexical Entrainment

I am seeing some promising initial results with lexical entrainment with BMIC that mirrors GME from Andreas's paper. For this week, I focused on the perplexity metric, and followed the procedure detailed in the paper: train a trigram language model for each speaker's lemmatized utterances, use each model to calculate the perplexity of their partner's utterances (partner), then use each model to calculate the perplexity of utterances made by those they did not speak with (other).

Using the above, the difference between partner and other perplexities is highly significant (3.4857 10^5) for games, but is insignificant for conversation, and insignificant for combined game and conversation data. My initial guess is to why this happens is that games involve collaborative back-and-forth discussions, often with game-specific terminology that both players reuse. Conversations tend to have more of a longer turn-taking structure, where one person spends time answering the prompt individually while the other listens before they switch roles. I guess if this is true then broadly speaking, it might be that having a storyteller/listener involves less lexical entrainment than having a goal-oriented problem-solving conversation.

I am going to continue with other lexical entrainment metrics, and also try to find a positive correlation between emotional entrainment and lexical entrainment.


### Acoustic-prosodic work with CGC
This is starting to concern me a little. I was partially unable to reproduce the 2011 paper's results with my own extracted features or the preprocessed features Andreas sent me. It's possible some of this has to do with the different structure of the data (it looks similar, but there are a few differences in how it is ordered and how sessions are structured), but I went through a couple of revisions and am still getting different results.

As an example, I chose to focus on synchrony because that was a major source of divergence between BMIC and 2011 CGC. Here are the results:

Feature| r (BMIC games) | p (BMIC games) | r (CGC 2011) | p (CGC 2011) | r (CGC Matt) | p (CGC Matt)
-------|----------|----------|---------|--------|---------|--------
Pitch (Mean)|0.0323|0.0117|0.28|≈ 0|-0.0122|0.4792
Pitch (Max)|0.0017|0.8924|0.18|≈ 0|0.0100|0.5609
Intensity (Mean)|-0.0089|0.4786|0.47|≈ 0|0.3217|1.2290 10<sup>-82</sup>
Intensity (Max)|-0.0357|0.0047|0.50|≈ 0|0.2802|2.5090 10<sup>-62</sup>
Jitter|0.0644|4.42603 10<sup>-6</sup>|0.23|≈ 0|0.0831|3.6349 10<sup>-6</sup>
Shimmer|0.0349|0.0144|0.16|≈ 0|0.0066|0.7155
NHR|0.0840|2.2935 10<sup>-11</sup>|0.23|≈ 0|0.0896|1.8284 10<sup>-7</sup>

Basically what I'm seeing is that, while results are closer in significance to the original study, not all features are significant. Additionally, where there is a significant linear correlation, it is not as positive a correlation as the original analysis.

I think the fact that I'm seeing some additional significance is good, and I feel like I should focus on some of the metrics that aren't as significant (there could be differences in how I'm calculating them). I will try to pair with Andreas again, and maybe there are files left over from the original 2011 analysis I can look at.

---

I worked on some basic statistical analysis of emotional and acoustic-prosodic entrainment this week. Here are some general results that are representative of what I'm seeing:

### General correlation

First, here are correlations between acoustic-prosodic features and valence/arousal.

|                  |      valence |    arousal |
|:-----------------|-------------:|-----------:|
| energy           | -0.0303773   |  0.221712  |
| pitch_mean       | -0.00283354  |  0.0365282 |
| pitch_std        |  0.0192358   | -0.0490368 |
| pitch_min        | -0.0444853   |  0.0535081 |
| pitch_max        |  0.00800468  |  0.030562  |
| intensity_mean   |  0.0141265   |  0.471361  |
| intensity_std    |  0.0380429   |  0.252555  |
| intensity_min    | -0.0388018   |  0.14006   |
| intensity_max    |  0.0265659   |  0.456163  |
| jitter           | -0.000196673 | -0.168203  |
| shimmer          | -0.00586974  | -0.127007  |
| harmonicity_mean | -0.0186542   |  0.152183  |
| harmonicity_std  | -0.0453533   |  0.0705816 |
| harmonicity_min  | -0.0738522   | -0.0944758 |
| harmonicity_max  |  0.0743613   |  0.179423  |
| rate             |  0.0250662   |  0.117837  |

Only arousal appears to have any kind of direct correlation with acoustic-prosodic features, and even then it is pretty weak except for intensity mean and max.


### Movement correlation

I wanted to see if acoustic-prosodic features move in tandem with valence and arousal. Using an approach similar to determining synchrony, I computed the difference across turns for both emotion and acoustic-prosodic features. These are the Pearson's correlation coefficients for those differences.

|                  |   valence_r |   valence_p |   arousal_r |    arousal_p |
|:-----------------|------------:|------------:|------------:|-------------:|
| energy           |  0.0241558  | 0.374099    |   0.214925  | 1.23651e-15  |
| pitch_mean       | -0.022234   | 0.413306    |  -0.0229985 | 0.397427     |
| pitch_std        |  0.048068   | 0.0768199   |  -0.0307456 | 0.257888     |
| pitch_min        | -0.075271   | 0.00555166  |  -0.0105636 | 0.697539     |
| pitch_max        |  0.0246529  | 0.364345    |   0.0280712 | 0.301632     |
| intensity_mean   |  0.112274   | 3.4183e-05  |   0.548947  | 1.45374e-107 |
| intensity_std    |  0.097231   | 0.000336278 |   0.299949  | 1.36997e-29  |
| intensity_min    |  0.00458931 | 0.865921    |   0.15442   | 1.09429e-08  |
| intensity_max    |  0.113881   | 2.63e-05    |   0.53805   | 1.30076e-102 |
| jitter           | -0.00556309 | 0.837832    |  -0.109768  | 5.10892e-05  |
| shimmer          | -0.0334022  | 0.218993    |  -0.0617459 | 0.0229782    |
| harmonicity_mean | -0.0101824  | 0.707943    |   0.0605966 | 0.025655     |
| harmonicity_std  | -0.0188743  | 0.487402    |   0.0290278 | 0.28545      |
| harmonicity_min  | -0.0847418  | 0.00178856  |  -0.135748  | 5.23705e-07  |
| harmonicity_max  |  0.0621771  | 0.0220382   |   0.187126  | 3.76287e-12  |
| rate             |  0.0357861  | 0.152493    |   0.157466  | 2.39999e-10  |


Takeaways:
* Change in arousal are much more strongly correlated with change in acoustic-prosodic features than movements in valence.
* Change in energy, mean intensity, intensity std, and intensity max are strongly linearly correlated with arousal. Change in speaking rate and max harmonicity are weakly linearly correlated with arousal. In addition, jitter is somewhat negatively correlated with arousal.
* In contrast, the only acoustic-prosodic features that change alongside valence are mean and max intensity, but with a weak linear correlation (approx. 0.11).

In general, features for arousal make sense to me. But because there are so few acoustic-prosodic features whose changes correlate with change in valence, I wonder what else could be behind it. Maybe lexical features?

---

### Final corrected acoustic-prosodic entrainment
This is where I spent most of my time this week. I think I finally ironed out the issues in my feature extraction pipeline (there were a few). Here are my results. I omitted speech rate for now - I will address that next. The goal with this was to complete an analysis of acoustic/prosodic entrainment as a starting point to compare it with emotional entrainment. Since I think I'm done with the analysis, I will work on comparing them this week.

**Global Convergence**

Feature| p (BMIC games) | p (CGC)
-------|----------|----------
Pitch (Mean)|0.0450|N.S.
Pitch (Max)|0.0109|N.S.
Intensity (Mean)|N.S.|0.01
Shimmer|N.S.|0.03
NHR|N.S.|0.002

Results are not siginficant in the BMIC for conversations or for combined conversations and games.

**Global Proximity**

Feature| p other (BMIC games) | p other (BMIC conversations) | p self (BMIC games) | p self (BMIC conversations) | p self (CGC) | p other (CGC)
-------|----------|----------|---------|--------|--------|--------
Pitch (Mean)|0.3220|0.0332|0.1986|0.0168|N.S.|1.7 10<sup>-05</sup>
Pitch (Max)|0.0685|0.1806|0.0338|0.1395|0.0008|N.S.
Intensity (Mean)|0.0120|0.9265|0.0085|0.8401|6.1 10<sup>-06</sup>|0.003
Intensity (Max)|0.0292|0.8648|0.0186|0.9560|0.0002|0.04
Jitter|0.23780|0.1696|0.5590|0.3273|N.S.|4.8 10<sup>-05</sup>
Shimmer|0.2083|0.4287|0.1165|0.5897|0.05|0.04
NHR|0.7009|0.9475|0.4035|0.5870|0.007|0.009

**Local Convergence**

Feature| r (BMIC games) | p (BMIC games) | r (CGC) | p (CGC)
-------|----------|----------|---------|--------
Pitch (Mean)|0.0094|0.4599|-0.06|4.6 10<sup>-11</sup>
Pitch (Max)|-0.0047|0.7099|-0.05|4.9 10<sup>-08</sup>
Intensity (Mean)|0.0444|0.0004|-0.03|0.0001
Intensity (Max)|0.0335|0.0079|-0.02|0.007
Jitter|-0.0163|0.2298|0.03|0.002
Shimmer|0.0090|0.5136|0.0008|N.S.
NHR|0.0296|0.0184|0.007|N.S.

BMIC conversations were only significant for two features:

Feature | r (BMIC conversations) | p (BMIC conversations)
--------|------------------------|-----------------------
Shimmer|-0.0677|0.0028
NHR|0.0442|0.0406


**Local Proximity**

Highly significant differences at turn changes vs. unrelated turns. Seen in BMIC and CGC for all features (pitch mean/max, intensity mean/max, jitter, shimmer, and NHR) for all session types (games and conversations)


**Local Synchrony**

Feature| r (BMIC games) | p (BMIC games) | r (CGC) | p (CGC)
-------|----------|----------|---------|--------
Pitch (Mean)|0.0323|0.0117|0.28|≈ 0
Pitch (Max)|0.0017|0.8924|0.18|≈ 0
Intensity (Mean)|-0.0089|0.4786|0.47|≈ 0
Intensity (Max)|-0.0357|0.0047|0.50|≈ 0
Jitter|0.0644|4.42603 10<sup>-6</sup>|0.23|≈ 0
Shimmer|0.0349|0.0144|0.16|≈ 0
NHR|0.0840|2.2935 10<sup>-11</sup>|0.23|≈ 0

For BMIC conversations, only mean pitch was significant with r=-0.0561 and p=0.0103.


**Takeaways and Questions**

We had discussed this before but basically there is not much similarity between the BMIC and CGC, but it probably isn't very important. The only highly significant result I got was synchrony, which happened on every feature. Others were hit or miss, with some results exhibiting some significance.

My questions:
1. Does this look right?
1. Are these results worth releasing by themselves?
    - They are what they are: put them in the literature to state what we found.
    - Contextualize them by comparing with other similar datasets: Fischer, Switchboard, CGC.
1. BMIC was partially based on CGC. If it's important, what is different about the BMIC that could have led to differences in results?

**To do**
Get checked transcripts from Andreas and use them to generate speaking rate.

### Paper
I'd like to talk about these in person.

**Option 1: Short conference paper (INTERSPEECH, March 30, 4 pages)**
Main goal is to introduce the BMIC. Present the emotion entrainment results as an example of a study we are doing with it, but do not include general acoustic/prosodic results yet (space concerns, also pending discussion of takeaways above.

**Option 2: Longer conference paper (~6 pages)**
Main goals are to introduce the BMIC and show work we are doing with it. Present the emotion entrainment results alongside acoustic/prosodic results (pending discussion of takeaways above). No set deadline, so time to work out kinks and do more with acoustic/prosodic-emotion entrainment correlations or whatever else we want to explore.


### Next steps
* Writing the paper: will start this week
* Correlating acoustic-prosodic features/entrainment with emotion features/entrainment: will continue this week
* What is different about the BMIC and the CGC that yielded different entrainment results, despite having a partially similar format?
    * Get fisher/switchboard/CGC and redo analysis there? Compare results?
* Attempt to recreate a conversation context paper using BMIC (longer term)

---

I found out I had an outdated version of the dataset, so I had to redo some analysis to bring in the up-to-date data. Additionally, I found out there were multiple annotation attempts, so I needed to rework how I was ingesting the data from the psiturk database. New results can be found here:

Session proximity with partner distance:

![Session proximity with partner distance](img/aa-session-proximity-partner.png)

Session proximity with self distance:

![Session proximity with partner distance](img/aa-session-proximity-self.png)

Turn proximity:

![Session proximity with partner distance](img/aa-turn-proximity.png)

Turn synchrony:

![Session proximity with partner distance](img/aa-turn-synchrony.png)

There was no significant evidence for convergence, either turn-level or session-level.

To answer an older outstanding question regarding averaging annotations within turns: only about 7.4% of turns have more than one annotation. There is not a statistically significant difference between the distribution of all turn annotations and the distribution of averaged intra-turn annotations. I think maybe averaging them out is OK. I'm not sure what else I can do because annotators actually leave different amounts of annotations per turn. For example, one might say there is one emotion, while another says there is two or three. I can think of some ways of doing a more detailed analysis accounting for this, but I'm not sure it's worth it right now.

I omitted the incomplete annotator's annotations from the dataset and it didn't seem to make much difference.

Some outstanding paper questions/thoughts:

* What is the best way to frame the outcome and introduction? How much of the 2011 Levitan/Hirschberg paper should I reference, and how much should I copy over?
* Is this the first introduction of this dataset? I should probably spend a while describing it - how much, and in how much detail? Get some paragraphs from Andreas?
* Still thinking about the missing annotations. I also had to omit a session due to technical reasons too.
* Emotion entrainment or affective alignment? The latter seems like it's used more.
* General framing questions - to discuss.


---

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