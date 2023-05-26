---
title: 'What Makes A Great Toggle Button? (Case Study, Part 2)'
slug: toggle-button-case-study-part-2
author: eduard-kuric
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3d25c3a9-5cbd-44e2-9c8c-742d35c261ee/toggle-button-case-study.png
date: 2022-08-29T14:00:00.000Z
summary: >-
  The problem of how to design an effective toggle button that shows the selected option clearly is a long-term open question among UI/UX designers. In this second part, Eduard Kuric explains a complex list of visual cues used by toggle buttons to communicate which of their options is active.
description: >-
  The problem of how to design an effective toggle button that shows the selected option clearly is a long-term open question among UI/UX designers. In this second part, Eduard Kuric explains a complex list of visual cues used by toggle buttons to communicate which of their options is active.
categories:
  - UI
  - UX
  - Usability
  - Case Studies
---

In the [first article of this two-parter](https://www.smashingmagazine.com/2022/08/toggle-button-case-study-part-1/), we have covered a crucial yet unresolved problem in UI design concerning toggle buttons. Getting across which option is active isn’t easy. There are many visual cue types to choose from: font style, colors, and outlines, just to name a few. To assess which visual cues communicate effectively the option toggled on, we have conducted a thorough case study with over 100 real users and 27 visual cues. Read on to learn about our findings and their implications to take away when designing toggle buttons of your own.

## Case Study Results

Let’s see what we found out about effective ways to put an emphasis on a button to make it clear that it’s active. But first, a quick summary of our participants.

### Participant Review

After our data collection was completed, we first had to review the quality of participants in our study. This review has led to the disqualification of some participants, mainly those who have shown signs of choosing the answers at random 50-50, a clear sign of not making an effort to complete the tasks genuinely. After we removed these offenders, we were left with the following numbers of participants per study:

<table>
	<thead>
		<tr>
			<th rowspan="2">Study type:</th>
			<th colspan="2">5-Second Test</th>
      <th colspan="2">20-Second Test</th>
		</tr>
	</thead>
	<tbody>
		<tr>
      <td><strong>Group:</strong></td>
			<td>1</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
		</tr>
		<tr>
      <td><strong>Number of participants:</strong></td>
			<td>28</td>
      <td>29</td>
      <td>30</td>
      <td>27</td>
		</tr>
	</tbody>
</table>

**Note:** *These numbers are still higher than the number of results that we set out to collect as the minimum since we accounted for a dropout rate of up to 16% while launching our recruitment online.*

### Metric For Comparing Utility Of Visual Cues

We conducted four studies with the tool [**Five Second Test**](https://www.uxtweak.com/five-second-test-tool). Two with a 5-second time limit and two with a 20-second limit. We needed a metric that could objectively compare toggles to each other and how a specific toggle fared in 5-second and 20-second test variants.

We created a weighted metric, which we named the Success-Confidence score. The Success-Confidence score is derived from the number of correct answers (according to expectations) combined with the Likert scale answers to the question: “How sure do you feel about your answer?”

First, we calculate the average confidence for correct and incorrect answers separately and for every toggle. Average confidence can range from 0 to 1 based on how participants answered the Likert scale question. For example, if every respondent who chose the correct toggle side were to respond with “Absolutely sure” on the Likert, the average confidence for the correct answers for the given toggle would be 1.

We then used the calculated average confidence for correct and incorrect answers and calculated the Success-Confidence score of the toggle by using the following formula:

<div class="break-out">

 <pre><code class="language-markup">Success-Confidence score = (correct_num * correct_conf) - (incorrect_num * incorrect_conf)

correct_num -> number of correct answers

incorrect_num -> number of incorrect answers for toggle

correct_conf -> average confidence with correct answers

incorrect_conf -> average confidence with incorrect answers 
</code></pre>
</div>

Since we had different numbers of participants available for each test, we normalized the Success-Confidence score by dividing it by the total number of participants for the given test. Resulting in the following formula:

**Normalized Success-Confidence score = Success-Confidence score / number of participants**

The scale of normalized Success-Confidence score is -1 to 1. Minus 1 designates a toggle where all participants provide wrong answers with high confidence, and 1 designates a toggle where all respondents answer correctly with high confidence.

{{% feature-panel %}}

### Evaluation Of Research Questions 

#### RQ 1: Bold text

A low error rate of 1.7% and a high Success-Confidence score of 0.86 confirmed our expectation that emboldened text in a toggle button makes options perceived as active compared to regular text. This version of the toggle even performed well enough to earn the **third best average rank among all the evaluated toggles**. Based on this result, we can safely pronounce bold text in the active button as a functional yet simple solution for communicating which toggle option is selected. This knowledge should be particularly useful if all your toggle buttons use fonts of equal weight, as is often the case.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c25a5cfa-a520-4a26-b076-dce65f6d1e9a/1-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c25a5cfa-a520-4a26-b076-dce65f6d1e9a/1-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c25a5cfa-a520-4a26-b076-dce65f6d1e9a/1-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Bold text" >}}

#### RQ 2: Text size

We tested four toggles with varying size differences between the text in the active and inactive buttons. As predicted, the toggle where the font size difference was barely noticeable performed the worst with an error rate of almost 15% and a confidence score of only 0.63. Compared to that, the toggle with the greatest difference in font size was perceived with an error rate of only 4.4% and a confidence score of 0.81, which are both significant improvements when compared to the smallest difference. The performance of the two middle toggles was set between these two extremes. Unexpectedly, the toggle with the second smallest difference slightly outperformed the toggle with the second greatest difference. However, this irregularity is small enough to be explained by noise in the data.

Since the performance rate grew in general with the font size, our expectation of “greater size difference means better visual cue for toggles” was confirmed. However, since using a significantly bigger font to represent the active state can prove to be visually unappealing, we suggest using bold text instead. **Bold text is not only easier to include in your design, but also performs better.**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5482070e-3e62-4931-a428-9fdd2a63f2c7/2-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5482070e-3e62-4931-a428-9fdd2a63f2c7/2-toggle-button-case-study-part-2.png" width="800" height="507" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5482070e-3e62-4931-a428-9fdd2a63f2c7/2-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="" >}}

#### RQ 3: Contrast of inverted colors in text labels

The black & white and orange & blue inverted color combinations proved to be some of the worst performing toggles we’ve tested, with error rates of 19.3% and 23.7% and confidence of only 0.56 and 0.41, respectively. The low confidence levels suggest that even the respondents who managed to select the correct answer weren’t confident at all in their answers. Our prediction of the darker colors perceived as active was confirmed by the error rate of less than 0.5 in both cases. However, the low confidence deteriorates the strength of the lower error rates. This means that our hypothesis that inverted font colors are an ineffective visual cue was confirmed. Try to avoid using colors of the same visual importance, as also seen in research question number 8 which concerns toggle backgrounds.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6c14b6-d5e1-43c5-95c5-db495a7af9ae/3-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6c14b6-d5e1-43c5-95c5-db495a7af9ae/3-toggle-button-case-study-part-2.png" width="800" height="240" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5d6c14b6-d5e1-43c5-95c5-db495a7af9ae/3-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="The black & white and orange & blue inverted color combinations" >}}

#### RQ 4: Cultural perception of red vs. green in text labels

A seemingly surprising (although not completely unexpected) result came from the toggle with red and green text. The error rate for this toggle is 32.5% and confidence only 0.32, making it one of the worst performing toggles overall, with an average rank of  24.67. This result suggests that the red/green combination not only fails to improve the results compared to other color couples but actually makes it worse. The possible explanation could be that the green color was perceived as a switch, not a sign of an active state. Red-green colorblindness is also the most common type of color vision deficiency, which is reason enough not to use this visual cue, as wrong answers in our experiment also reflect.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e212e571-f160-45f1-9ba2-0428c2685abe/4-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e212e571-f160-45f1-9ba2-0428c2685abe/4-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e212e571-f160-45f1-9ba2-0428c2685abe/4-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Red & green in text labels" >}}

#### RQ 5: Color vs. black/white in text labels

The combination of colorful and white labels performed well (avg rank of 9.33). The toggle which was surprisingly problematic was the combination of color and black. This toggle with an error rate of 14% and confidence of only 0.59 shows that the participants weren’t able to pick the active side reliably. We predict that this phenomenon was most likely caused by the visual strength of black text compared to colored text, regardless of hue. Therefore, simply distinguishing active and inactive toggles by turning inactive black text colorful isn’t recommended. For better color-based approaches, simply continue reading our findings for the next research questions.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9f413c-4649-4a7e-93c7-e934332f6442/5-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9f413c-4649-4a7e-93c7-e934332f6442/5-toggle-button-case-study-part-2.png" width="800" height="240" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8c9f413c-4649-4a7e-93c7-e934332f6442/5-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Color vs. black/white in text labels" >}}

#### RQ 6: Primary color vs. neutral color (shades of gray) in text labels

Compared to the toggles from the immediately preceding research question, this toggle represents a middle ground between the white and black inactive options with its gray color. This was reflected in the resulting average rank of 12, which is better than the color vs. black option, but worse than color vs. white.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11d851c3-1318-433f-820c-d12eea109214/6-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11d851c3-1318-433f-820c-d12eea109214/6-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/11d851c3-1318-433f-820c-d12eea109214/6-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Yellow & gray in text labels" >}}

#### RQ 7: Different saturation of the same color in text labels

The last text color variant of toggles we tested also confirmed our theory. The difference in saturation was a strong enough cue to secure satisfying results (an error rate of 8.7% with a confidence of 0.77). This suggests that the respondents reliably selected the correct option. Note that while the error rate was comparable to primary vs. neutral color, different saturations of the same color inspired higher confidence. Therefore, the preferable option is to use a lower saturation of the same color instead of greyscale for inactive toggle buttons.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5652dc62-f6fa-4d36-858d-2cb99e634705/7-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5652dc62-f6fa-4d36-858d-2cb99e634705/7-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5652dc62-f6fa-4d36-858d-2cb99e634705/7-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Different saturation of the same color in text labels" >}}

#### RQ 8: Contrast of inverted colors in the background and RQ 9: Cultural perception of red and green in the background

The toggles defined in these hypotheses were counterparts to the toggles from hypotheses 3 and 4. We kept the color pairs the same, but this time we filled the toggle’s backgrounds with the color instead of coloring the text. The results with background colors followed the same pattern as with the text, with the black-&-white combination performing the best, the orange-&-blue coming second and red-&-green taking last place. However, compared to the colored text variants, the filling variants performed better than their text alternative (error rate improvement by 5-8%).

What may seem counterintuitive at first is that although black-&-white filling has a stronger potential to stimulate confusion due to dark/light mode settings, it still performed better than black-&-white text alternative or inverted colors with hue. How a light/dark mode setting would affect the results for this specific toggle could bear further investigation. However, for building an optimal toggle, it might be unnecessary, considering the overall better results achieved by other types of toggle backgrounds.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b717b094-8964-4ba3-8e9b-222ce3a02c4a/8-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b717b094-8964-4ba3-8e9b-222ce3a02c4a/8-toggle-button-case-study-part-2.png" width="800" height="240" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b717b094-8964-4ba3-8e9b-222ce3a02c4a/8-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Contrast of inverted colors in background" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a51bb2-fe44-489d-a054-5ec0c489e437/9-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a51bb2-fe44-489d-a054-5ec0c489e437/9-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/62a51bb2-fe44-489d-a054-5ec0c489e437/9-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Red and green in backgroun" >}}

#### RQ 10: Different saturations of the same color in the background

Different shades of orange achieved an error rate of 9.7% and a normalized Success-Confidence score of 0.72. Compared to that, different shades of gray had an error rate of 15% and a normalized Success-Confidence score of 0.63 for the gray toggle &mdash; both overall decent scores which proved these visual cues as usable. The improvement of the orange color over the greyscale variant has been significant (resulting in an average rank of 13.67 compared to 18). It is important to note that even though the orange variant performed better than the gray one, their performance was still average at best. If background colors are used in this form, we recommend combining them with another visual cue.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078c3e9b-715d-4719-ae51-997562b8c451/10-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078c3e9b-715d-4719-ae51-997562b8c451/10-toggle-button-case-study-part-2.png" width="800" height="240" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/078c3e9b-715d-4719-ae51-997562b8c451/10-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Different saturations of orange and gray" >}}

#### RQ 11: Saturated colors and grayscale colors in the background

As expected, the version where the inactive button was a lighter shade of gray performed better (6.1% error rate and 0.79 confidence) than the darker gray version (12.3% error rate and 0.66 confidence). It also outperformed the orange version from hypothesis 10 and overall performed well, earning the average rank of 6.67 (sixth best). The more saturated version was placed in the bottom half but still managed to outperform the grayscale version from hypothesis 10 (average rank 15 compared to 18). The results of these two hypotheses suggest that if we want to use a saturated color fill to denote activity, it is best coupled with low saturated gray.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ae8dcf-d419-4f23-9727-f2812e8b4bf0/11-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ae8dcf-d419-4f23-9727-f2812e8b4bf0/11-toggle-button-case-study-part-2.png" width="800" height="240" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4ae8dcf-d419-4f23-9727-f2812e8b4bf0/11-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Saturated colors and grayscale colors in background" >}}

#### RQ 12: Inverted design of buttons

We believed that the inversion of design would be more confusing to the users than the saturations described in hypotheses 10 and 11. With a 6.1% error rate and 0.78 Success-Confidence score, this toggle ranks just below the best saturation variant (saturated color and less saturated gray), scoring seventh place overall with an average rank of 7.33. However, it is important to note that this toggle performed significantly worse in the 20-second test compared to the 5-second test (a drop of 9 between the rankings). This can be explained by the fact that the half with the filled background (the correct one to pick) lures the user’s attention very quickly (resulting in better performance on a 5-second test). However, when the user is provided with a longer time to observe the toggle, they start to question their instincts, resulting in a more than doubled error rate (from 3.5% to 8.8%). Therefore, we recommend avoiding inversion of toggle buttons in favor of visual cues that avoid potential confusion and don’t highlight the inactive button in any way.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c60ae1f-fe33-40d7-8757-6b03994e8389/12-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c60ae1f-fe33-40d7-8757-6b03994e8389/12-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4c60ae1f-fe33-40d7-8757-6b03994e8389/12-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Inverted design" >}}

#### RQ 13: Highlighted outline of the active button

As expected, the highlighted outline provided a reliable cue for respondents to decide (8.8% error rate and 0.76 Success-Confidence score). The average rank of 10 puts this toggle in the top half of toggles performance-wise. Due to being outperformed by other visual cues, a combination with another cue is recommended for better visual clarity.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8808f412-adad-4857-b14f-85d3d68bd7c5/13-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8808f412-adad-4857-b14f-85d3d68bd7c5/13-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8808f412-adad-4857-b14f-85d3d68bd7c5/13-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Highlighted outline of the active button" >}}

#### RQ 14: Inactive button coincides with the background

Another exciting result. Although we suspected that the respondents could have problems perceiving the inactive button as a button at all, this toggle achieved stellar results. With an error rate of only 0.9% and confidence of more than 0.89, it ranked first overall with an average rank of 1.33, which is an improvement over the simple saturated color vs. grayscale toggle seen in RQ11. This means that having the inactive button of the same color as the surroundings is a supreme way to communicate selection in a toggle button.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Inactive button coincides with the background" >}}

#### RQ 15: Embossed vs. debossed button

The error rate for both embossed toggles was 83.3% and the confidence score was the same as well with -0.58. This means that chasing skeuomorphism isn’t always the right solution, at least when it comes to toggles.

We expect this result is due to the common use of embossing effects in digital interfaces to bestow more weight on interface elements. A toggle with more visual weight would be perceived as active. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b152d-67da-49b1-80bf-9b9294e37953/15-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b152d-67da-49b1-80bf-9b9294e37953/15-toggle-button-case-study-part-2.png" width="800" height="268" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/267b152d-67da-49b1-80bf-9b9294e37953/15-toggle-button-case-study-part-2.png'>Large preview</a>)" alt=" Embossed vs. debossed button" >}}

#### RQ 16: Check sign

As expected from its straightforward nature, the check sign icon added to an active button in a toggle performed very well, achieving the **second best average rank** of 2.33 with only a 5% error rate on Success-Confidence score of 0.86. The only problem we see in choosing this toggle is its potential cumbersome inclusion in the design of the web, and it may induce unwanted connections with checkboxes.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="A check sign icon" >}}

#### RQ 17: Radio button

Even though the nature of the radio button toggle is similar to the check sign design, when used as an icon, its meaning is less explicit. This was confirmed by achieving a worse average rank of 5.67 and a higher error rate of 9% combined with a lower Success-Confidence score of only 0.8. Despite the rather good performance of this visual cue, using radio buttons as toggles doesn’t align with their semantics since the radio buttons are meant to be used in forms, while toggles are meant to signify an immediate change of state. 

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d67cef10-3ebb-4ceb-b542-1233ed888266/17-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d67cef10-3ebb-4ceb-b542-1233ed888266/17-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d67cef10-3ebb-4ceb-b542-1233ed888266/17-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Radio Button" >}}

{{% ad-panel-leaderboard %}}

### Ranking The Visual Cues

We ranked the visual cues represented by toggles separately for the results they achieved in 5-second tests, 20-second tests, and the two combined. This resulted in 3 separate rankings. We calculated the average rank for every toggle and came up with the three worst and three best toggles.

#### Worst Toggles

**Third last place &mdash; Toggle #9 &mdash; Red & Green Text Labels**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40eb4d0-dc8d-428e-b17a-95e1a3378640/18-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40eb4d0-dc8d-428e-b17a-95e1a3378640/18-toggle-button-case-study-part-2.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b40eb4d0-dc8d-428e-b17a-95e1a3378640/18-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Red & Green Text Labels" >}}

- **Average rank: 24.67**
- 5-second test rank: 25
- 20-second test rank: 24
- Combined rank: 25

**Second last place &mdash; Toggle #22 &mdash; Embossed button (no shadow version)**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e560dcb0-9890-4c82-9e14-2ec8eda09335/19-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e560dcb0-9890-4c82-9e14-2ec8eda09335/19-toggle-button-case-study-part-2.png" width="800" height="118" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e560dcb0-9890-4c82-9e14-2ec8eda09335/19-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Embossed button (no shadow version)" >}}

- **Average rank: 26.33**
- 5-second test rank: 27
- 20-second test rank: 26
- Combined rank: 26

**Last place &mdash; Toggle #27 &mdash; Embossed button (shadow version)**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f38454c-f56b-4fad-b06b-254aea788952/20-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f38454c-f56b-4fad-b06b-254aea788952/20-toggle-button-case-study-part-2.png" width="800" height="137" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f38454c-f56b-4fad-b06b-254aea788952/20-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Embossed button (shadow version)" >}}

- **Average rank: 26.67**
- 5-second test rank: 26
- 20-second test rank: 27
- Combined rank: 27

#### Best Toggles

**Third place winner &mdash; Toggle #2 &mdash; Bold text**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16175d5b-ae00-48a8-9c9a-9a567b10b5b6/21-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16175d5b-ae00-48a8-9c9a-9a567b10b5b6/21-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/16175d5b-ae00-48a8-9c9a-9a567b10b5b6/21-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Bold text button" >}}

- **Average rank: 2.67**
- 5-second test rank: 4
- 20-second test rank: 2
- Combined rank: 2

**Second place winner &mdash; Toggle #24 &mdash; Check sign**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png" width="800" height="" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/88067f25-e570-470b-80a0-92849dfdfa5d/16-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Check sign button" >}}

- **Average rank: 2.33**
- 5-second test rank: 1
- 20-second test rank: 3
- Combined rank: 3

**First place winner &mdash; Toggle #26 &mdash; Inactive button coincides with the background**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/170e853d-e235-4aba-bfc8-c17f105a0b63/14-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Inactive button coincides with the background" >}}

- **Average rank: 1.33**
- 5-second test rank: 2
- 20-second test rank: 1
- Combined rank: 1

### Difference between the 5-second and 20-second test

Our secondary goal was to learn the difference in perception of toggles based on the time the respondents had to observe them, before deciding on an answer. Our expectation was that the result from the 20-second tests should be better overall (lower error rate and higher confidence score) than the results of the 5-second tests since the participants would have more time to think about the toggles in front of them.

**We have calculated the average values and the results can be seen in the following table:**

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Test type</th>
			<th>Average error rate</th>
      <th>Average n. confidence score</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>5-second test</td>
			<td>0.1728</td>
      <td>0.5749</td>
		</tr>
		<tr>
			<td>20-second test</td>
			<td>0.1670</td>
      <td>0.6013</td>
		</tr>
	</tbody>
</table>

The results confirmed our expectations since the average error rate was lower in the 20-second tests and the Success-Confidence score was higher. However, these differences were not significant. What interested us was whether any specific toggles showed significant differences between the two test variants. Therefore we focused on toggles that showed the biggest improvements/deteriorations between the 5-second and 20-second test results.

#### Toggles that performed better after 20 seconds

The greatest improvement in the number of ranks gained between a 5-second and a 20-second test is shared between toggles #4, #11, and #18 seen below. They all gained 6 ranks once participants had more time to observe them. This signifies that the clarity of the cues improved with added observation time.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07bbbf2-1ec9-4abe-910a-a9da4e89428c/24-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07bbbf2-1ec9-4abe-910a-a9da4e89428c/24-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c07bbbf2-1ec9-4abe-910a-a9da4e89428c/24-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Button with small font size difference between the active and inactive state" >}}

- 5-second test rank: 16
- 20-second test rank: 10
- Error Rate Difference: -0.0527
- Normalized Success-Confidence Score Difference: 0.0913

This visual cue had the second smallest font size difference between the active and inactive states. We believe the change in rank is due to some participants needing time to notice smaller font size differences. However, the difference was noticeable enough to matter when the additional time was added to the test. 

The next two toggles have enough in common for us to analyze them together.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c58f4d02-b34d-41fc-b0c5-15a2e8a08e81/25-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c58f4d02-b34d-41fc-b0c5-15a2e8a08e81/25-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c58f4d02-b34d-41fc-b0c5-15a2e8a08e81/25-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Blue and white text labels" >}}

- 5-second test rank: 12
- 20-second test rank: 6
- Error Rate Difference: -0.0526
- Normalized Success-Confidence Score Difference: 0.0912

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6383b3b-c5bf-4166-b7a1-285b34f68f93/26-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6383b3b-c5bf-4166-b7a1-285b34f68f93/26-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f6383b3b-c5bf-4166-b7a1-285b34f68f93/26-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="A button with different shades of orange" >}}

- 5-second test rank: 17
- 20-second test rank: 11
- Error Rate Difference: -0.0526
- Normalized Confidence Score Difference: 0.0772

Both these cues were designed in a way that the more pronounced/saturated color denotes the active option while the inactive option is portrayed by a lighter color. The difference in results shows that a certain percentage of users initially view a lighter color as the more pronounced one. However, the percentage decreases when users spend more seconds thinking about the toggle. To make a toggle that is easy to comprehend right away, an interface designer should probably look at the other visual cues.

#### Toggles that performed worse after 20 seconds

**Toggle 15**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f36d4edf-f168-4c03-9f6a-96bb0907f48a/27-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f36d4edf-f168-4c03-9f6a-96bb0907f48a/27-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/f36d4edf-f168-4c03-9f6a-96bb0907f48a/27-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="Black and white text labels" >}}

**Toggle 17**

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93acc796-7bc7-475e-a946-3fa33b7b3f8f/28-toggle-button-case-study-part-2.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93acc796-7bc7-475e-a946-3fa33b7b3f8f/28-toggle-button-case-study-part-2.png" width="800" height="107" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/93acc796-7bc7-475e-a946-3fa33b7b3f8f/28-toggle-button-case-study-part-2.png'>Large preview</a>)" alt="A button with different shades of gray" >}}

<table class="tablesaw break-out">
	<thead>
		<tr>
			<th>Toggle Number</th>
			<th>5-second test rank</th>
      <th>20-second test rank</th>
      <th>Error Rate Difference</th>
      <th>N. Confidence Score Difference</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>15</td>
			<td>11</td>
      <td>19</td>
      <td>0.0526</td>
      <td>-0.1018</td>
		</tr>
		<tr>
			<td>17</td>
			<td>15</td>
      <td>21</td>
      <td>0.0877</td>
      <td>-0.1299</td>
		</tr>
	</tbody>
</table>

Toggle 15 showed the biggest drop in rank, while toggle 17 suffered the most significant negative changes in error rate and confidence score.

We explain the drop in these two by the fact that these two toggles are similar in a way &mdash; both have a dark and a light half &mdash; which means they would be perceived differently, for example, when using the light mode versus dark mode setting on a mobile device. While the user’s instinctive reaction may be to pick the darker color as active, given some time, more people will begin to second-guess themselves. Instead of the darker color capturing their gaze, they may start overthinking that the brighter color is highlighted against the dark. A good toggle shouldn’t encourage such doubts.

{{% ad-panel-leaderboard %}}

## Potential For Future Research

All the cues we tested in our study were simple/singular. Going from here, the natural next step for research would be to go deeper, with a study that focuses on evaluating our findings in more detail: *Can I use a bold font in an inactive toggle button if the inactive button is even bolder? Will the combination of visual cues perform better than either cue individually?* While the answers may seem intuitive, research data may prove otherwise, as our study has shown.

Another next step would be testing the effect of color alterations. Would the saturation of green work just as well as the saturation of orange?

Testing the performance of visual cues in prototypes of website navigation using different color schemes is another ambitious area for continued research. We tested our toggles in the void, but it’s possible that their performance would vary depending on the visual context.

## Conclusion

In this article, we described our research where we analyzed a complex list of visual cues used by toggle buttons to communicate which of their options is active. By testing our research questions with real users, we collected a respectable amount of data to make reliable statements about the effectiveness of visual cues.

Here are some of the main points we arrived at that you should keep in mind when designing your next toggle button:

- If you choose to use **color** as the main lead, we suggest you **use a combination of a saturated lively color** (ideally corresponding with your CTA color scheme) **and a light grayscale neutral color**. Using the colors in the toggle’s background fill is preferable to using colored text. If the color of the inactive button is the same as the surrounding background, this will further improve the button’s comprehensibility.
- **Contrasting colors of similar visual weight should not be used under any circumstances**. Red and green’s cultural perceptions won’t help you communicate what’s selected. There are much better ways to go about this. Be wary of the black and white combination as well. Toggles that use this color scheme are the ones most prone to the confusion rooted in the dark/light mode settings.
- You may choose a minimalistic path and use the **font** itself to show the difference between button states. The **bold-thin combination is the go-to solution**, but you may also use different font sizes. Just make sure to differentiate the font sizes well enough. Using font-weight or size is recommended to support other visual cues as well since it’s very flexible.
- If you decide to use embossment as the main cue &mdash; you really shouldn’t. It proved to be unreliable at communicating the active state of a toggle. Even a simple border was more effective. If you decide to use embossed toggles for their visual appeal, we suggest combining embossment with a primary visual cue, such as bold text or color fill. 
- There’s no shame in using designs that you are sure will work. A tick or a radio-button icon both performed very well. The evident drawback of choosing them is the cumbersome inclusion in the design of your web since radio buttons as UI elements serve a different function from toggles. The ticks could be perceived as outdated (akin to a physical form more than a website). As for radio button icons, you might as well use a radio button instead.

Follow these tips, and your toggle button designs will no longer cause users to hesitate about what’s selected at the moment. 

### Resources

- “[Why Toggle Buttons Are Confusing](https://uxmovement.medium.com/why-toggle-buttons-are-confusing-544e3e46ec1d)”, UX Movement
- “[History Of Toggle + UI/UX Case Study + UI Samples](https://www.behance.net/gallery/70302039/History-Of-Toggle-UIUX-Case-Study-UI-Samples)”, Ramulu Nelli
- “[Stop Misusing Toggle Switches](https://uxmovement.com/mobile/stop-misusing-toggle-switches/)”, UX Movement
- [1991 Video Of The HCIL Touchscreen Toggle Switches (University of Maryland)](https://www.youtube.com/watch?v=wFWbdxicvK0)
- “[What’s The Most Effective Way To Present Two-State Toggle Buttons?](https://www.researchgate.net/publication/317182817_What’s_the_Most_Effective_Way_to_Present_Two-State_Toggle_Buttons)”, Thomas Tullis, Azilah Iskandar, Lori Ledoux
- [Color Theory In Web UI Design](https://www.uxpin.com/studio/ebooks/color-theory-web-ui-design-practical-principles/)
- [UX Research Tools](https://www.uxtweak.com/)

{{< signature "vf, yk, il" >}}
