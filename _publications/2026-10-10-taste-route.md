---
title: "TasteRoute: Personalized Routing for Video Generation"
collection: publications
permalink: /publication/2026-10-10-taste-route
excerpt: 'Even the consensus of other annotators agrees with an individual user''s favorite video generator only 34-55% of the time. We introduce TasteRoute, a personalized router that selects a video generation model based on the request, user preferences, and generation budget, and release TasteRoute-3k, a human-annotated dataset of multi-model video comparisons, preference rankings, and user-profile signals.'
date: 2026-10-05
category: conferences
venue: 'arXiv preprint'
paperurl: 'https://arxiv.org/abs/2610.05896'
citation: 'Tam, Z.R., Wu, C.C., Yang, S.H., Ku, P., Kuang, B., Hsieh, T.T., Hsu, M.F., Tsai, F.L., Chen, Y.N., Ma, W.C., &amp; Lin, C.Y. (2026). &quot;TasteRoute: Personalized Routing for Video Generation.&quot; arXiv preprint arXiv:2610.05896.'
---

Video generation has come a long way, but choosing which model to use is still surprisingly difficult. Different generators have different strengths, and their prices vary substantially. We study the less-explored problem of routing among video generators: choosing a model for a particular request, user, and budget.

![Will Smith eating spaghetti, 2023 to 2026](/images/will-smith-spaghetti.gif){: .align-center}

So given a request (like prompt or image + prompt), which video model should be used to generate it? The natural answer is "send it to whichever model people like best". However after we have collected human preferences data, taste turned out to be surprisingly personal: even when the consensus of all the other annotators is used as an oracle, it agrees with an annotator's own favorite only 34-55% of the time. There is no single best video model for everyone, and the models differ a lot in how much each generation costs.

People mostly agree on which videos are bad, but much less on which one is best. When a comparisons involve a rejected video, annotators agree 83-85% of the time. When both videos are acceptable and free of flagged defects, agreement drops to 57-62%. In one example, the consensus winner was everybody's second choice and nobody's favorite. This motivated us to collect quality judgments separately from personal preference rankings.

![The consensus winner was everyone's second choice, while each annotator picked a different favorite](/images/exec-ba7028c8-8ee1-46e7-b3b9-62a8bcb913ac.webp)

So we built TasteRoute, a personalized router that makes its choice before generating any video. It encodes the prompt and optional reference image, then scores candidate generators using a ranking model trained on preference feedback. The personalized version learns from an individual user's own comparisons. At inference time, we filter out generators above the budget and choose the highest-ranked affordable option.

![How TasteRoute works: understand the request, personalize, filter by budget, then route](/images/exec-c368eb2f-87ee-4f74-9c61-872e5726a09e.webp)

Across text-to-video and image-to-video settings, TasteRoute's general routing performance is comparable to a strong nearest-neighbor baseline. Personalization becomes more useful as the budget expands and more generators become affordable. At budget caps of $1.00, $1.50, and $2.00 per video, TasteRoute-Personal achieves the highest ranking quality over affordable candidates and the lowest average generation cost among the compared routers. Its cost savings range from 8-12% relative to the most expensive alternative at each cap. Interestingly, the main router is trained without a cost penalty: these savings emerge because learning users' preferences sometimes leads to choosing cheaper generators.

User feedback also matters. In our label-scaling experiment, TasteRoute-Personal overtakes a pooled router trained on the same number of prompt groups at around 10 groups, and a nearest-neighbor baseline using the same user's feedback by 50 groups. With very little feedback, the simpler baselines remain strong choices.

We are also releasing [TasteRoute-3k](https://huggingface.co/datasets/appier-ai-research/tasteroute-3k), containing 3,128 annotated videos across 394 requests: 274 text-to-video and 120 image-to-video. The videos are drawn from a catalog of 30 generator endpoints. Nine annotators, including five professional video creators, supplied quality assessments and individual preference rankings. We preserve those individual judgments alongside onboarding preference signals so others can study both shared quality requirements and differences in taste.

There is still plenty left to solve. On video pairs where users express opposite preferences, TasteRoute currently only reaches 55.2% accuracy, showing that directly conflicting tastes remain difficult to predict. Our results only covered nine annotators with fixed generator catalog, and the observed savings reflect their preferences rather than a guarantee that personalization always reduces cost. I personally also think learning preferences that generalize to more users and changing model catalogs is an important next step.

<a href='https://arxiv.org/abs/2610.05896'>Download paper here</a>
