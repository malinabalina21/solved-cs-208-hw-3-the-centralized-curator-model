Download Link: https://assignmentchef.com/product/solved-cs-208-hw-3-the-centralized-curator-model
<br>
<strong>Instructions: </strong>Submit a single PDF file containing your solutions, plots, and analyses. Make sure to thoroughly explain your process and results for each problem. Also include your documented code and a link to a public repository with your code (such as GitHub/GitLab). Make sure to list all collaborators and references.

<ol>

 <li><strong>Tails, Trimming, and Winsorization: </strong>In all of the parts below, the dataset is <em>x </em>∈ {0<em>,</em>1<em>,…,D</em>}<em><sup>n</sup></em>. In all of the implementation parts, you should write code that takes as input <em>D </em>∈ N, <em>n </em>∈ N, <em>x </em>∈ {0<em>,</em>1<em>,…,D</em>}<em><sup>n</sup></em>, and <em>ε &gt; </em>

  <ul>

   <li>Prove that the following algorithm for estimating a Trimmed mean is <em>ε</em>-DP and implement it in code:</li>

  </ul></li>

</ol>

+ Lap<em> ,</em>

where <em>P<sub>.</sub></em><sub>05 </sub>and <em>P<sub>.</sub></em><sub>95 </sub>are the 5th and 95th percentile of the dataset. That is, we are applying the Laplace mechanism after removing the bottom and top 5% of the dataset. (Hint: Think about Lipschitz constants.)

<ul>

 <li>Prove that for large enough <em>n</em>, the analogous algorithm for the <em>Winsorized </em>mean is <em>not ε</em>-DP:</li>

</ul>

+ Lap<em>,</em>

where [ is defined as in Problem Set 2. In Winsorization, we clamp points rather than dropping them. (In class on 3/11, we incorrectly referred to dropping points as Winsorization.) Again, it may be useful to first think in terms of Lipschitz constants.

<ul>

 <li>In class, we saw how to use the exponential mechanism to an estimate of the median, <em>P<sub>.</sub></em><sub>5</sub>. Describe and implement a version of the exponential mechanism that releases an estimate of the <em>t</em>th percentile <em>P<sub>t </sub></em>of a dataset <em>x </em>∈ {0<em>,…,D</em>}<em><sup>n </sup></em>any desired <em>t </em>∈ [0<em>,</em>100]. (A direct implementation of the exponential mechanism would require explicitly calculating weights for each of the <em>D </em>+ 1 possible outputs, which can be too slow for large values of <em>D </em>such as in the parts below. One way to solve this is to bin the elements into fixed, coarser intervals. Alternatively, you can sample more quickly from the output distribution of the exponential mechanism by noting that if you sort the elements of the dataset <em>x<sub>i</sub></em><sub>1 </sub>≤ <em>x<sub>i</sub></em><sub>2 </sub>≤ ··· ≤ <em>x<sub>i</sub></em><em><sub>n</sub></em>, then all elements of each interval between <em>x<sub>i</sub></em><em><sub>j </sub></em>and <em>x<sub>i</sub></em><em><sub>j</sub></em><sub>+1 </sub>have the same weight, so you can sample by choosing an interval with probability proportional to the sum of weights within it and then sampling uniformly from that interval. Feel free to use either solution below.)</li>

 <li>Implement the following <em>ε</em>-DP algorithm for estimating a Trimmed mean of a dataset: use your algorithm from Part 1c to get <em>ε/</em>3-DP estimates <em>P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>05 </sub>and <em>P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>95 </sub>of the 5th and 95th percentiles, drop all datapoints that lie outside the range [<em>P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>05</sub><em>,P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>95</sub>], and then use the Laplace mechanism to compute an (<em>ε/</em>3)-DP mean of the trimmed data. That is, your code should compute</li>

</ul>

+ Lap<em> .</em>

<ul>

 <li>Determine whether or not the following analogue for a Winsorized mean is <em>ε</em>-DP: use Part 1c to get <em>ε/</em>3-DP estimates <em>P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>05 </sub>and <em>P</em><sup>ˆ</sup><em><sub>.</sub></em><sub>95 </sub>of the 5th and 95th percentiles, and output</li>

</ul>

+ Lap <em> .</em>

You do not need to formally prove your answer, but you should at least provide an informal explanation.

<ul>

 <li>The dataset csv provides the 5% PUMS Census file for Massachusetts. For <em>ε </em>= 1 and <em>D </em>= 1<em>,</em>000<em>,</em>000, compare the RMSE between DP means and the actual means for each PUMA in Massachusetts,<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> for DP means calculated using (i) the ordinary Laplace mechanism for a mean (remembering to clamp your data to the range!) and (ii) the algorithm from Part 1d. Also show box-and-whisker plots of the DP released means for each PUMA by these algorithms, noting the true means. You should probably order these by mean income, or perhaps skew of income, or anything you think reveals an interesting pattern. Give an intuitive explanation of the kinds of datasets on which algorithm (i) is likely to perform better than algorithm (ii) and vice-versa. Describe any modifications you might propose would increase the utility (at the same level of privacy preservation) for data similar to this income example.</li>

</ul>

<ol start="2">

 <li><strong>Composition: </strong>Suppose you have a global privacy budget of <em>ε </em>= 1 (and are willing to tolerate <em>δ </em>= 10<sup>−9</sup>) and you want to release <em>k </em>count queries (i.e. sums of Boolean predicates<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>) using the Laplace mechanism with an individual privacy loss of <em>ε</em><sub>0</sub>. By basic composition, you can set</li>

</ol>

<em>ε</em><sub>0 </sub>= <em>ε/k</em>. Using the advanced composition theorem, you can set <em>ε</em><sub>0 </sub>= <em>ε/</em><sup>p</sup>2<em>k </em>ln(1<em>/δ</em>). We have provided you with code from PSI for the “optimal” composition theorem for differential privacy that calculates the largest value of <em>ε</em><sub>0 </sub>that ensures global (<em>ε,δ</em>)-DP as a function of <em>ε</em>, <em>δ</em>, and <em>k</em>.<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a>For each of these choices, plot (on the same graph) the standard deviation of the Laplace noise added to each query as a function of <em>k</em>, and find the smallest values of <em>k </em>where the advanced and optimal composition theorems strictly improve upon the basic composition theorem.

<ol start="3">

 <li><strong>Synthetic Data: </strong>Expanding the template from class, and using again csv, create a DP three-way histogram<a href="#_ftn4" name="_ftnref4"><sup>[4]</sup></a> release of income, education and age. You do not need to graph this histogram, just compute the release for each binned combination of the variables. From this, you should be able to generate synthetic data of these three variables. Run a linear regression</li>

</ol>

as a post-process on your synthetic data, predicting income from education and age<a href="#_ftn5" name="_ftnref5"><sup>[5]</sup></a> using the equation:

Income<em><sub>i </sub></em>= <em>β</em><sub>0 </sub>+ <em>β</em><sub>1</sub>Education<em><sub>i </sub></em>+ <em>β</em><sub>2</sub>Age<em><sub>i </sub></em>+ <em>ν<sub>i</sub></em>;                  <em>ν<sub>i </sub></em>∼ N(0<em>,σ</em><sup>2</sup>)                               (1)

Let  be the coefficients in the full sensitive data, while <em>β</em><sup>˜ </sup>the DP release we generate. The mean-squared error of a DP release of <em>β</em><sup>˜ </sup>can be decomposed into the contributions of bias and variance as:

MSE(<em>β</em><sup>˜</sup>) = bias(<em>β</em><sup>˜</sup>)<sup>2 </sup>+ var(<em>β</em><sup>˜</sup>) = (E[<em>β</em><sup>∗ </sup>− <em>β</em><sup>˜</sup>])<sup>2 </sup>+ E[(<em>β</em><sup>¯˜ </sup>− <em>β</em><sup>˜</sup>)<sup>2</sup>]                                   (2)

For this calculation, we are taking the (sensitive) regression coefficients <em>β</em><sup>∗ </sup>on the entire dataset as the true values of <em>β</em>. Show the contributions to MSE of the bias and variance of the DPregression coefficients.<a href="#_ftn6" name="_ftnref6"><sup>[6]</sup></a>

As a baseline to decide if these squared bias and error terms are large, we can compute the MSE due simply to sampling, by bootstrapping with replacement new datasets in which we compute new (sensitive) regression estimates <em>β</em><sup>ˆ </sup>on the bootstrapped data and compute MSE(<em>β</em><sup>ˆ</sup>). How do the bias and variance terms due to creating DP-releases compare to the this numerical estimate of the error introduced by sampling?

<ol start="4">

 <li><strong>BONUS: </strong>Using your developed understanding of differential privacy, and the described use case in the Gaboardi <em>et al. </em>PSI paper, reexamine the deployed instance of the PSI budgeting tool, available at <a href="http://psiprivacy.org/">http://psiprivacy.org</a><a href="http://psiprivacy.org/">.</a> Provide any feedback that you think would make the interface easier for the intended non-expert “data owner” user to budget a DP-release, or would otherwise improve the system. (Note: Insightful, considered feedback will receive 1/2 point bonus, and feedback that strikes us a revelatory or particularly intriguing idea will receive 1 point bonus and a note of thanks in a future paper draft.)</li>

 <li><strong>Final Project: </strong>By <strong>April 9</strong>, submit a couple of pages giving a detailed description of what your final project will look like. You should be able to clearly state your research questions, briefly articulate how your project relates to what has been done in the past, describe the approach you are taking, give your timeline for completing various aspects of the project, and <em>discuss your fallback plan in case you don’t obtain the results that you’re hoping to obtain</em>.</li>

</ol>

<a href="#_ftnref1" name="_ftn1">[1]</a> You can assume that the N in each PUMA is public information.

<a href="#_ftnref2" name="_ftn2">[2]</a> A Boolean predicate is a function that returns a 0 or a 1. An example of a count query might be the sum of bits for all college students.

<a href="#_ftnref3" name="_ftn3">[3]</a> See the function update parameters in <a href="https://github.com/privacytoolsproject/cs208/blob/master/examples/wk5_centralized/psiExamples.r">/examples/wk5</a> <a href="https://github.com/privacytoolsproject/cs208/blob/master/examples/wk5_centralized/psiExamples.r">centralized/psiExamples.r</a> or <a href="https://github.com/privacytoolsproject/cs208/blob/master/examples/wk5_centralized/psiExamples.ipynb">psiExamples.ipynb</a><a href="https://github.com/privacytoolsproject/cs208/blob/master/examples/wk5_centralized/psiExamples.ipynb">.</a>

<a href="#_ftnref4" name="_ftn4">[4]</a> That is, a histogram representation counting the occurrences of having all possible combinations of the three binned variables.

<a href="#_ftnref5" name="_ftn5">[5]</a> You will likely find that log(income) has a more linear relationship with your other two variables, so feel free to shift from income to log(income) if you prefer. However, you will need to decide how to treat zero values in income; one option is to clip the lower bound of income to some small positive value.

<a href="#_ftnref6" name="_ftn6">[6]</a> To numerically compute the expectations, simply repeat your simulation many times and average.