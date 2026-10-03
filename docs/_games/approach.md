[🔙](../../README.md#research)

# Approach 🧭

What this repository is for, which problem each cited paper leaves open, and what the repository does about that problem. The input and the confirmation gate are the [log contract](log-contract.md).

This is a proof of concept of a method. A developer submits a real GameAnalytics export and receives a reading tied to those events, after confirming what the game-specific names mean. It is not a result from a shipped game.

The four analyses are exploration, risk-taking, experimentation, and play style. Each one judges telemetry the caller supplies and returns a score, a separate confidence, the evidence, and the data quality. Counts and sequences are computed from the confirmed events. Each analysis follows this page and the log contract.

&nbsp;

[🔝](#approach-🧭)

## The problems, and what this repository does

**A metric is not an experience.** Yannakakis, Spronck, Loiacono, and André [1] show that gameplay metrics observe experience only indirectly: little interaction can be captivation or boredom, and a model that ignores the game context infers the wrong state. Pedersen, Togelius, and Yannakakis [2] predicted fun, challenge, frustration, and related states from gameplay statistics plus level parameters, checked against forced-choice self-reports. Challenge and frustration were predictable. Fun was harder. The same signal, such as a death, raised challenge and frustration differently. This repository does not predict fun, arousal, or frustration. A result keeps observation, measurement, inference, and interpretation apart, and it names the game conditions the reading depends on.

**A model from one game does not travel by itself.** Shaker, Shaker, and Abou-Zleikha [3] hand-generalized features across a platformer and a shooter and could predict engagement, frustration, and challenge on the combined data. Features that did not mean the same thing in both games, such as gap width, did not survive that translation. Melhart, Liapis, and Yannakakis [4] predicted a change in arousal across unseen games inside one genre from abstract features such as time, score, and input diversity. Time dominated. They do not claim the result across genres. This repository uses a construct on more than one game only where the studio has confirmed that the event ids share a meaning.

**Totals hide order, and a button press does not travel.** Chen, Seif El-Nasr, Canossa, Badler, Tignor, and Colvin [5] argue that aggregate counts discard the sequence of choices, and that two players can share level and time while differing in order. Their sequences tracked expertise more than personality. Bakkes, Spronck, and van Lankveld [6] show that an action model fails when the same style is played with a different set of buttons, while a tactic or strategy description travels further and predicts less specifically. Exploration, risk-taking, and experimentation read sequences and choices. Play style summarizes those three readings plus progression and resource patterns. None of them emit a personality score.

**Exploration depends on the goal and the reward in the session.** Gómez-Maureira, Kniestedt, van Duijn, Rieffe, and Plaat [7] found that level-design patterns raised spatial exploration, that an explicit goal and being paid reduced it, and that a curiosity trait did not predict who explored. Acevedo, Choi, Liu, Kao, and Mousas [8] found that a coin-collection task lowered the share of the map players visited. The exploration analysis reports off-path and optional activity under the mapping, and it reports a missing goal or reward as missing context instead of as a low score.

**A general risk questionnaire is a weak fit to match behavior.** Lyu, Zhao, Zhang, Chen, Zhou, and Zhu [9] paired Dota 2 matches with a general risk-propensity questionnaire. The best model explained about 17% of the questionnaire. Risk-taking here records a harder option taken while a safer one was available in the mapped log, and it keeps that choice separate from the outcome. A failure is not, by itself, risk-taking.

**What to measure is decided with the game's own mechanics.** Seif El-Nasr [10] describes gameplay telemetry as four facts on every action — what, where, when, and who — and treats the useful features as the ones tied to the core mechanics, chosen with the people who designed the game. The questions a designer can check are which areas are over- or under-used, which features are not used as intended, and where progression sticks. That choice is the mapping interview in the log contract. The agent asks only about design events the schema does not already explain.

**The designer gets a readable account tied to the events.** Rubio-Manzano and Triviño [11] turn gameplay numbers into sentences through rules the designer defined, so a session is not only a scoreboard. This repository writes the account for the developer, and every sentence traces to the measurements. It does not invent a label the events do not support.

**Motivation types are not computed from the stream.** Voitovich [12] states the gap between telemetry, which records what players do, and motivation models, which talk about why, and offers a research agenda rather than a solved prediction. This repository does not assign a motivation type.

&nbsp;

[🔝](#approach-🧭)

## What a designer receives

For a confirmed export, a report with:

- a score and a separate confidence for each analysis that had enough mapped evidence
- the events, counts, and sequences that support it
- the data quality: how many events and sessions, and whether goal, reward, or a safer alternative was present
- a note on what a designer might check, kept separate from the measurement

Where the evidence is thin or the context is missing, the report says so and leaves the score out.

&nbsp;

[🔝](#approach-🧭)

## References

[1] G. N. Yannakakis, P. Spronck, D. Loiacono, and E. André, "Player Modeling," in *Artificial and Computational Intelligence in Games*, Dagstuhl Follow-Ups, 2013.

[2] C. Pedersen, J. Togelius, and G. N. Yannakakis, "Modeling Player Experience for Content Creation," *IEEE Transactions on Computational Intelligence and AI in Games*, vol. 2, no. 1, pp. 54–67, 2010. https://doi.org/10.1109/TCIAIG.2010.2043950

[3] N. Shaker, M. Shaker, and M. Abou-Zleikha, "Towards Generic Models of Player Experience," in *Proceedings of the AAAI Conference on Artificial Intelligence and Interactive Digital Entertainment*, vol. 11, no. 1, 2015. https://doi.org/10.1609/aiide.v11i1.12806

[4] D. Melhart, A. Liapis, and G. N. Yannakakis, "Towards General Models of Player Experience: A Study Within Genres," in *IEEE Conference on Games*, 2021. https://arxiv.org/abs/2110.00978

[5] Z. Chen, M. Seif El-Nasr, A. Canossa, J. Badler, S. Tignor, and R. Colvin, "Modeling Individual Differences through Frequent Pattern Mining on Role-Playing Game Actions," in *Proceedings of the AAAI Conference on Artificial Intelligence and Interactive Digital Entertainment*, vol. 11, no. 5, pp. 2–7, 2015. https://doi.org/10.1609/aiide.v11i5.12847

[6] S. C. J. Bakkes, P. H. M. Spronck, and G. van Lankveld, "Player behavioural modelling for video games," *Entertainment Computing*, vol. 3, no. 3, pp. 71–79, 2012. https://doi.org/10.1016/j.entcom.2011.12.001

[7] M. A. Gómez-Maureira, I. Kniestedt, M. van Duijn, C. Rieffe, and A. Plaat, "Level Design Patterns That Invoke Curiosity-Driven Exploration: An Empirical Study Across Multiple Conditions," *Proceedings of the ACM on Human-Computer Interaction*, vol. 5, no. CHI PLAY, article 271, 2021. https://doi.org/10.1145/3474698

[8] P. Acevedo, M. Choi, H. Liu, D. Kao, and C. Mousas, "Game Level Design to Evoke Spatial Exploration: The Influence of a Secondary Task," in *Companion Proceedings of the Annual Symposium on Computer-Human Interaction in Play*, 2024. https://doi.org/10.1145/3665463.3678811

[9] S. Lyu, N. Zhao, Y. Zhang, W. Chen, H. Zhou, and T. Zhu, "Predicting Risk Propensity Through Player Behavior in DOTA 2: A Cross-Sectional Study," *Frontiers in Psychology*, vol. 13, 2022. https://doi.org/10.3389/fpsyg.2022.827008

[10] M. Seif El-Nasr, "Intro to User Analytics," *Game Developer*, 2013. https://www.gamedeveloper.com/business/intro-to-user-analytics

[11] C. Rubio-Manzano and G. Triviño, "Automatic Linguistic Feedback in Computer Games," in *Proceedings of the 2015 Conference of the International Fuzzy Systems Association and the European Society for Fuzzy Logic and Technology*, 2015. https://doi.org/10.2991/ifsa-eusflat-15.2015.69

[12] I. Voitovich, "Integrating Telemetry with Player Motivation Models," in *Conference Proceedings of DiGRA Central Asia*, 2026. https://dl.digra.org/index.php/dl/article/view/2777

&nbsp;

[🔙](../../README.md#research)
