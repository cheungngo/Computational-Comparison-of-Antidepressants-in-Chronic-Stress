# Structural Rebuilding Confers Superior Long-Term Resilience: A Unified Multi-Mechanism Computational Comparison of Antidepressants in Chronic Stress

Authors:

Ngo Cheung, FHKAM(Psychiatry)

Affiliations:

¹ Independent Researcher

Corresponding Author:

Ngo Cheung, MBBS, FHKAM(Psychiatry)

Hong Kong SAR, China

Tel: 98768323

Email: info@cheungngomedical.com

**Conflict of Interest**: None declared.

**Funding Declaration**: This research received no specific grant from
any funding agency in the public, commercial, or not-for-profit sectors.

**Ethics Declaration**: Not applicable.

Citation:
Cheung, N. (2026). Structural Rebuilding Confers Superior Long-Term Resilience: A Unified Multi-Mechanism Computational Comparison of Antidepressants in Chronic Stress. Zenodo. https://doi.org/10.5281/zenodo.18295517


## Abstract

Background: Major depressive disorder remains inadequately treated in
many patients, with divergent onset speeds and durability across
antidepressant classes. Emerging neuroplasticity frameworks emphasize
synaptic loss, yet direct computational comparisons of glutamatergic
(ketamine-like), monoaminergic (SSRI-like), and GABAergic
(neurosteroid-like) mechanisms---particularly under chronic stress---are
lacking.

Methods: We extended a pruning-plasticity model by applying 95%
magnitude-based synaptic elimination to overparameterized feed-forward
networks trained on Gaussian cluster classification. From identical
pruned states, three interventions were tested across 10 stochastic
seeds: ketamine-like gradient-guided regrowth (50% reinstatement) with
consolidation; SSRI-like prolonged low-learning-rate refinement with
gradual noise reduction; and neurosteroid-like global tonic inhibition
(30% damping plus bounded activations). Outcomes included acute
recovery, stress resilience (graded internal noise), acute relapse
(additional 40% pruning), and longitudinal durability (eight cycles of
10% cumulative pruning with mechanism-specific maintenance).

Results: All treatments restored near-ceiling baseline performance, but
resilience diverged: ketamine-like networks showed superior
extreme-noise tolerance (81.7%) and zero acute/longitudinal relapse
across seeds, despite rising sparsity. SSRI-like refinement yielded
moderate gains (81.3% combined-stress acutely) but 40% seed relapse
longitudinally. Neurosteroid-like inhibition matched early efficacy
(97.8%) yet exhibited state-dependence and late-cycle vulnerability (20%
seed relapse).

Conclusions: These simulations demonstrate mechanistically distinct
routes---structural rebuilding (durable), gradual optimization
(variable), reversible stabilization (rapid but fragile)---yielding
predictive trade-offs in relapse risk. Findings support mechanism-based
personalization, prioritizing synaptogenic agents for severe/chronic
cases while rationalizing combinations for acute relief and maintenance.

## Introduction

Major depressive disorder (MDD) is one of the top drivers of global
disability and carries heavy personal and financial costs \[1\]. Even
with many drugs on the market, progress has stalled: only about a third
of patients get well after an initial prescription, and roughly a third
remain symptomatic after several different regimens \[2\]. Selective
serotonin re-uptake inhibitors (SSRIs) still dominate routine care, yet
these medicines often take weeks to work and may deliver only partial
relief \[3\].

The hunt for faster and more dependable options has reshaped the field.
Low-dose ketamine, an NMDA-receptor blocker, can lift mood within hours.
The effect was known to be tied to bursts of synaptogenesis through
BDNF- and mTOR-linked pathways \[4,5\]. Neuroactive steroids such as
brexanolone and its oral analogue zuranolone increase tonic GABA_A
inhibition and also act quickly, most clearly in postpartum depression
\[6\]. These findings shift attention away from simple monoamine
shortage toward problems in neural plasticity: chronic stress trims
dendritic spines and synapses in prefrontal and hippocampal areas,
leaving circuits fragile \[7\].

Computational models let researchers test how such circuit changes might
play out. One influential idea treats depression as \"too much
pruning.\" The network still works under light load, but a small dose of
extra noise makes it fail. Earlier work showed that letting the model
regrow connections---an in-silico stand-in for ketamine---can restore
stability without rebuilding every lost synapse \[8\]. What remains
unclear is how different drug classes stack up when they are placed in
the same framework. Do they differ in speed? Durability? Risk of pushing
the system toward the opposite pole, as in a manic switch?

To explore those questions, we extended the pruning-plasticity model in
a simple feed-forward classifier. From identical 95 % pruned starting
points we applied three distinct interventions:

- a ketamine-like, gradient-guided regrowth routine;

<!-- -->

- an SSRI-like, slow refinement with fading noise;

- a neurosteroid-like, global increase in tonic inhibition.

The protocol ran across ten random seeds and eight sequential \"stress
cycles,\" adding more pruning each time to mimic chronic relapse
pressure. By following the same networks over time, we could compare
recovery, stability, and switch liability side by side. The aim was to
clarify how mechanism shapes outcome and to suggest when a given class
might be the better clinical choice as rapid, plasticity-targeted
treatments gain traction.

## Methods

### Network architecture and classification task

We built a small, fully connected feed-forward network to stand in for
cortical circuitry. The model held two input units, three hidden layers
(512, 512, 256 units) and four soft-max outputs. Hidden units used ReLU
unless noted otherwise. After each hidden layer we could inject
zero-mean Gaussian noise to mimic stress and, when needed, multiply
activations by a global damping factor to imitate tonic inhibition.

The task was simple on purpose (Figure 1). Two-dimensional points were
drawn from four Gaussian clouds centred at (−3, −3), (3, 3), (−3, 3) and
(3, −3) with a standard deviation of 0.8. For every random seed we
produced 12 000 training points, 4 000 noisy test points and 2 000 clean
test points. This layout let us watch accuracy fall as pruning and noise
mounted, a laboratory version of latent vulnerability described in
clinical work \[8,7\].

![](media/image1.png){width="5.140199037620297in"
height="6.839799868766404in"}

***Figure 1:** Computational Architecture of the Multi-Mechanism
Antidepressant Experiment. The diagram illustrates the information flow
through the StressAwareNetwork. Synthetic classification data is fed
into a feed-forward neural network. The \"Pathology Model\" simulates
depression via chronic stress, resulting in severe synaptic pruning (95%
sparsity). The network is then subjected to three distinct algorithmic
interventions: Ketamine-like structural regrowth, SSRI-like functional
weight stabilization, and Neurosteroid-like inhibitory modulation. The
system evaluates the resilience of each mechanism against relapse over 8
longitudinal cycles of recurring stress.*

### Baseline training and pruning

Weights were drawn from a small normal distribution and the network
learned for 20 epochs with Adam (learning rate 0.001) on clean data.
Once accuracy steadied, we lopped off the weakest 95 % of weights across
all layers, leaving their sign intact. The result was a sparse
\"depressed\" circuit that still did the job when inputs were noise-free
but collapsed when perturbations appeared.

### Antidepressant treatment protocols

Starting from identical pruned copies we imposed three separate recovery
routines.

Ketamine-like synaptogenesis: For 30 mini-batches we collected gradient
magnitudes at every pruned site. The top half of those locations were
regrown with small random values (SD 0.03). Fifteen fine-tuning epochs
followed (Adam, lr 0.0005) while the new sparsity mask stayed fixed.

SSRI-like gradual stabilisation: Sparsity remained at 95 %. The model
trained for 100 epochs at a very low rate (1 × 10⁻⁵). Internal noise
began at σ 0.5 and faded linearly to zero, echoing the slow receptor and
transcription shifts seen with monoaminergic drugs \[9\].

Neurosteroid-like tonic inhibition: We kept the 95 % mask but switched
hidden activations to tanh and multiplied them by 0.7, reproducing the
dampening effect of extrasynaptic GABA_A modulation. Ten consolidation
epochs were run with Adam (lr 0.0005).

### Evaluation metrics

After each intervention we measured accuracy on four test sets: clean,
standard noisy, a combined-stress set (input noise σ 1.0 plus internal
noise σ 0.5) and a sweep of internal noise from σ 0.0 to 2.5.

Acute relapse was probed by pruning a further 40 % of the remaining
weights and retesting on the combined-stress set. For the neurosteroid
condition we also checked accuracy after turning the damping factor off
to see how much benefit depended on continued inhibition.

### Long-term relapse under chronic stress

Durability was followed across eight stress cycles (Figure 2). Each
cycle removed 10 % of the surviving weights, then applied a brief
maintenance step that matched the original mechanism:

- ketamine-like, five fine-tuning epochs;

<!-- -->

- SSRI-like, twenty very low-rate epochs with mild tapering noise;

- neurosteroid-like, ten epochs under active inhibition.

Combined-stress accuracy was recorded after every cycle. Dropping below
80 % marked a relapse.

### Reproducibility and statistics

All experiments were repeated with 10 different random seeds that
altered data draws, weight starts and noise streams. Means and standard
deviations are reported; we also quote the range where it was
informative. Code was written in PyTorch and run on a CPU; deterministic
options were fixed whenever the library allowed.

![](media/image2.png){width="6.268099300087489in"
height="6.77799978127734in"}

***Figure 2:** Longitudinal Relapse Simulation Protocol. The diagram
details the 8-cycle simulation used to evaluate long-term resilience.
Initial post-treatment models enter a recursive loop representing the
passage of time under adverse conditions. In every cycle, models undergo
\"Chronic Stress\" (cumulative magnitude-based pruning removing 10% of
remaining weights), followed by a mechanism-specific maintenance phase
(periodic regrowth for Ketamine, stress-scheduled stabilization for
SSRIs, or inhibitory consolidation for Neurosteroids). Relapse is
defined as a drop in classification accuracy below 80%.*

## Results

### Post-treatment recovery and baseline efficacy

Before any rescue procedure the heavily pruned networks were barely
functional: across ten seeds their accuracy under combined input and
internal noise averaged 28.9 % (SD 2.4 %). Once an intervention was
applied, performance on noise-free or mildly noisy data returned to
ceiling levels. The ketamine-style regrowth and the neurosteroid-style
tonic inhibition each produced perfect scores on both clean and standard
noisy sets and almost full recovery under the combined-stress condition
(97.3 % ± 0.2 and 97.8 % ± 0.1, respectively). The SSRI-style slow
refinement helped far less. Although many seeds reached high values on
clean inputs (mean 97.5 %, SD 7.6 %), their mean accuracy under combined
stress was only 81.3 % (SD 8.8 %), revealing large between-seed spread
(Table 1).

***Table 1.** Post-Treatment Efficacy (Mean ± SD Across 10 Seeds)*

|                    |              |             |              |                     |
|--------------------|--------------|-------------|--------------|---------------------|
| Treatment          | Sparsity (%) | Clean (%)   | Standard (%) | Combined Stress (%) |
| Untreated (pruned) | 95.0 ± 0.0   | 32.1 ± 11.8 | 32.3 ± 11.0  | 28.9 ± 2.4          |
| Ketamine-like      | 47.5 ± 0.0   | 100.0 ± 0.0 | 100.0 ± 0.0  | 97.3 ± 0.2          |
| SSRI-like          | 95.0 ± 0.0   | 97.5 ± 7.6  | 95.7 ± 8.0   | 81.3 ± 8.8          |
| Neurosteroid-like  | 95.0 ± 0.0   | 100.0 ± 0.0 | 100.0 ± 0.0  | 97.8 ± 0.1          |

### Resilience to graded internal stress

When internal noise was increased stepwise, the three regimens separated
sharply (Table 2). Ketamine-treated networks coped well even at the
harshest perturbation level (σ = 2.5), still classifying 81.7 % (SD 3.0
%) of patterns correctly. The SSRI-treated and neurosteroid-treated
models were similar up to moderate noise but both collapsed when noise
became severe, each settling near 41--42 % accuracy. Untreated baselines
hovered around chance throughout the sweep.

***Table 2.** Stress Resilience Profile (Mean ± SD Accuracy)*

|                    |              |                      |                  |                    |                     |
|--------------------|--------------|----------------------|------------------|--------------------|---------------------|
| Treatment          | No Noise (%) | Moderate (σ=0.5) (%) | High (σ=1.0) (%) | Severe (σ=1.5) (%) | Extreme (σ=2.5) (%) |
| Untreated (pruned) | 32.3 ± 11.0  | 29.2 ± 2.8           | 29.2 ± 1.6       | 28.9 ± 1.5         | 27.8 ± 1.6          |
| Ketamine-like      | 100.0 ± 0.0  | 99.9 ± 0.0           | 98.9 ± 0.7       | 95.3 ± 1.6         | 81.7 ± 3.0          |
| SSRI-like          | 95.7 ± 8.0   | 85.0 ± 9.6           | 66.2 ± 7.7       | 53.8 ± 5.6         | 42.0 ± 3.1          |
| Neurosteroid-like  | 100.0 ± 0.0  | 99.9 ± 0.1           | 91.6 ± 1.5       | 69.1 ± 2.0         | 41.2 ± 1.0          |

### Acute relapse vulnerability

A sudden removal of 40 % of the surviving weights served as an acute
relapse test. Ketamine-like models were almost unaffected, losing only
0.0 % on average (SD 0.4 %) from their combined-stress score. By
contrast, SSRI-treated networks dropped 9.1 % (SD 5.8 %) and
neurosteroid-treated networks dropped 6.9 % (SD 5.6 %).

### Neurosteroid state-dependence

The benefit of the neurosteroid analogue depended on continued tonic
damping. Once the damping factor was switched off, combined-stress
accuracy fell sharply to 68.8 % (SD 9.9 %). Interestingly, tolerance of
extreme internal noise improved slightly in this unmedicated state (51.9
% ± 2.8 versus 41.2 % ± 1.0 while medicated).

### Longitudinal trajectories under chronic stress

Eight cycles of additional 10 % pruning, each followed by a
mechanism-specific maintenance step, produced very different long-term
pictures (Table 3). Ketamine-like networks held steady around 97.6 %
combined-stress accuracy all the way to cycle 8 even though sparsity
rose from 47.5 % to 77.4 %. SSRI-treated models, which started low,
improved slowly and finished at 93.2 % (SD 2.0 %). Neurosteroid-treated
models looked excellent through the first five cycles but then diverged;
by cycle 8 the group mean had slipped to 88.2 % with a wide 49.6--97.7 %
range.

***Table 3.** Combined-Stress Accuracy (%) by Cycle (Mean ± SD)*

|       |            |            |              |
|-------|------------|------------|--------------|
| Cycle | Ketamine   | SSRI       | Neurosteroid |
| 0     | 97.5 ± 0.2 | 80.8 ± 8.7 | 97.7 ± 0.2   |
| 1     | 97.6 ± 0.2 | 84.7 ± 7.9 | 97.9 ± 0.3   |
| 2     | 97.7 ± 0.2 | 87.7 ± 5.4 | 97.8 ± 0.1   |
| 3     | 97.7 ± 0.3 | 90.1 ± 4.0 | 97.6 ± 0.4   |
| 4     | 97.6 ± 0.3 | 91.5 ± 3.4 | 97.5 ± 0.8   |
| 5     | 97.6 ± 0.4 | 92.1 ± 2.9 | 97.0 ± 0.9   |
| 6     | 97.5 ± 0.3 | 92.9 ± 2.4 | 95.6 ± 3.5   |
| 7     | 97.7 ± 0.3 | 92.6 ± 2.6 | 94.7 ± 2.8   |
| 8     | 97.6 ± 0.4 | 93.2 ± 2.0 | 88.2 ± 14.0  |

### Long-term relapse risk

***Table 4.** Longitudinal Relapse Summary*

|                                     |             |              |              |
|-------------------------------------|-------------|--------------|--------------|
| Metric                              | Ketamine    | SSRI         | Neurosteroid |
| Total accuracy drop (cycle 0 to 8)  | -0.1 ± 0.3% | -12.4 ± 8.3% | 9.5 ± 14.0%  |
| Final accuracy (cycle 8)            | 97.6 ± 0.4% | 93.2 ± 2.0%  | 88.2 ± 14.0% |
| Seeds with relapse (\<80%)          | 0/10        | 4/10         | 2/10         |
| Seeds without relapse (≥80%)        | 10/10       | 6/10         | 8/10         |
| Mean cycle at relapse (if relapsed) | N/A         | 0.0          | 8.0          |

None of the ketamine-treated seeds ever fell below the 80 % relapse
threshold (Table 4). Four SSRI-treated seeds crossed that line
immediately after the initial treatment, while two neurosteroid-treated
seeds relapsed late, in cycle 8. Averaged across seeds, total loss of
accuracy from cycle 0 to cycle 8 was −0.1 % for the ketamine analogue,
−12.4 % for the SSRI analogue, and +9.5 % for the neurosteroid analogue
(the plus sign reflects the sharp late decline after earlier gains).

Overall, relative to the 28.9 % baseline, the ketamine-like and
neurosteroid-like strategies each delivered an improvement of roughly 69
percentage points under combined stress, whereas the SSRI-like routine
lifted accuracy by about 52 points and displayed the greatest
variability and relapse liability.

## Discussion

### Interpretation of results

Placing three distinct recovery programmes inside the same wounded
network revealed a set of trade-offs that echo real-world pharmacology
(Figure 3). The ketamine-like routine, which reinstated half of the
deleted synapses in an activity-guided way, produced almost immediate
normalisation and---with or without further stress---barely budged
thereafter. Even when another forty per cent of the remaining weights
were cut and eight additional pruning rounds were imposed, accuracy
stayed above 97 % and no seed relapsed. Clinically, a single ketamine
infusion can trigger BDNF- and mTOR-dependent spine growth that outlasts
drug exposure and holds up under subsequent stress \[5,4\]. The model
suggests that durability arises not from a wholesale return to
pre-morbid density but from selectively restoring high-value links,
thereby rebuilding \"reserve\" that buffers later insults.

The SSRI-like schedule, by contrast, left the sparse architecture
untouched and relied on slow parameter drift while internal noise
tapered. Immediate gains were modest and uneven---some seeds barely
moved off the 30 % baseline---yet most improved gradually and several
reached the mid-90 % range by the final cycle. Four networks, however,
never achieved a secure foothold and slipped below the 80 % relapse line
early on. This mirrors the familiar picture of selective serotonin
re-uptake inhibitors: effectiveness that emerges over weeks, large
patient-to-patient variability, and a sizeable minority of
non-responders \[10,9\]. The simulation implies that when synaptic loss
is severe, merely \"tuning\" existing weights may be insufficient unless
accompanied by structural repair.

![](media/image3.png){width="6.268099300087489in"
height="5.597199256342957in"}

***Figure 3:** Comparative Mechanisms of Action and Resilience Profiles.
A schematic representation of the three distinct recovery pathways
observed in the simulation. The Ketamine-like pathway (left, blue)
confers lasting resilience by rebuilding synaptic \"reserve\" via
activity-guided regrowth, mirroring BDNF-dependent structural repair.
The SSRI-like pathway (center, orange) relies on tuning existing
weights; while effective for some, it exhibits high variability and
vulnerability when structural loss is too severe to be compensated by
parameter drift alone. The Neurosteroid-like pathway (right, green)
provides immediate functional relief via global gain control, but this
benefit is contingent on the presence of the agent, failing to prevent
relapse once the modulation is removed from a structurally deficient
network.*

The neurosteroid-like intervention offered the quickest subjective
relief---performance snapped back to healthy levels the moment tonic
damping was engaged---but the benefit proved contingent on continued
inhibition. Removing the damping cut combined-stress accuracy by nearly
thirty points, and two seeds collapsed during the last stress cycle
despite maintenance sessions. Clinical experience with brexanolone and
zuranolone is similar: fast symptom relief that can wane once dosing
stops, particularly if underlying circuitry has not had time to rebuild
\[6\]. In the model, global gain control contained excitability but, as
pruning progressed, there were simply too few functional pathways left
to stabilise.

Together, these findings support a neuroplasticity account of major
depression in which both the quantity and the quality of synapses
determine outcome \[11\]. When loss is extensive, agents that drive new
growth confer lasting insurance; modulators that optimise or damp
existing connections help only while enough structure remains---or while
the drug is present. The wide seed-to-seed spread observed for
monoaminergic and, later, neurosteroid conditions hints that individual
differences in baseline pruning depth or excitability may underlie the
heterogeneous responses seen in clinics.

### Clinical decision-making and personalised sequencing

The simulation outcomes map neatly onto everyday prescribing dilemmas
and suggest a triage logic based on underlying circuit damage and the
urgency of symptom relief.

Profound structural loss---often seen in chronic, highly recurrent or
treatment-resistant depression---appears best addressed with
synaptogenic drugs. In the model, the ketamine analogue restored
performance almost immediately, remained stable under extreme
perturbation, and never relapsed even after further 30--40 % pruning.
These features mirror clinical reports that a short ketamine course can
trigger durable remission through rapid BDNF--mTOR-dependent spine
formation \[12\]. For patients who repeatedly fail monoaminergic agents
or present with marked cognitive blunting or anhedonia, glutamatergic
treatments therefore deserve early consideration.

Situations demanding swift containment---postpartum depression, imminent
suicide risk, or severe agitation---may profit from neurosteroid
modulators. In silico, the GABAergic routine normalised accuracy in a
single step and maintained high scores through the first stress cycles,
echoing the clinical speed of brexanolone and zuranolone \[6\]. The
sharp decline after damping withdrawal, however, cautions that such
agents are bridges rather than stand-alone long-term solutions;
follow-up therapy should be organised before discontinuation.

When illness is less entrenched and baseline circuitry largely intact,
conventional SSRIs remain useful. Their simulated trajectory---slow but
steady gains, substantial variability and occasional early
failure---parallels real-world response curves. A poor initial
trajectory may signal the need for augmentation rather than a prolonged
wait-and-see approach.

Combined strategies emerge naturally from the model. Neurosteroids can
cover the latency of SSRIs; ketamine-guided regrowth can be followed by
low-dose SSRIs or psychotherapy to consolidate new connections; booster
ketamine sessions can reinforce reserve in highly stress-exposed
patients.

The contrasting relapse rates---zero for synaptogenic rescue versus
20--40 % for purely functional modulation---also argue for integrating
biomarkers of synaptic loss or neuroinflammation into routine assessment
so that clinicians can choose a mechanism informed by pathophysiology
rather than by trial-and-error.

### Novelty and translational potential

By embedding three fundamentally different antidepressant strategies
inside one pruning-plasticity model, this study offers a clearer look at
how treatment mechanism shapes both early response and long-term course
(Figure 4). Previous in-silico work usually explored one pathway at a
time---ketamine-like regrowth, slow monoaminergic adaptation, or global
inhibitory damping---making cross-class comparisons indirect at best.
Running the three approaches side-by-side from identical, over-pruned
baselines shows that the routes to recovery are not interchangeable.

![](media/image4.png){width="6.268099300087489in"
height="4.930699912510936in"}

***Figure 4:** Methodological Novelty and Translational Framework. This
diagram illustrates how the study\'s specific design choices (blue)
enable new analytical capabilities (orange), leading to distinct
mechanistic insights (green) that culminate in clinical utility
(purple). Unlike previous isolated studies, the Unified Framework allows
for direct comparison, revealing that recovery pathways are distinct
rather than interchangeable. The Multi-Seed Design captures stochastic
variability, linking relapse to baseline circuit integrity rather than
drug class alone. Finally, the Chronic Stress Extension demonstrates
that while functional fixes can fail over time, structural repair offers
lasting protection, providing a quantified rationale for selecting
treatments based on the trade-off between speed, durability, and
state-dependence.*

The multi-seed design is equally important. Introducing stochastic
variation revealed patterns that a single deterministic run would miss:
some \"patients\" on the SSRI schedule never cross a therapeutic
threshold, whereas a minority on the neurosteroid schedule crash only
after many stress cycles. Such divergence echoes clinical heterogeneity
and suggests that baseline circuit integrity or excitability, rather
than transmitter class per se, may determine who ultimately relapses.

The chronic-stress extension adds another layer. Few computational
studies have asked what happens after the first remission; here,
progressive pruning plus minimal \"maintenance\" demonstrates why
structural rebuilding protects every seed, whereas purely functional
fixes leave a tail of late failures. These findings dovetail with the
growing view that major depression reflects circuit-level
dysconnectivity, not merely monoamine shortage \[11\]. Quantifying the
trade-offs---speed versus durability versus state-dependence---gives
clinicians a mechanistic rationale for selecting ketamine, SSRIs,
neurosteroids, or combinations according to individual risk profiles.

### Limitations

Several caveats must temper direct biological inference. A feed-forward
network cannot reproduce the reverberating loops of corticolimbic
circuits; magnitude-based pruning is only a proxy for microglial or
inflammatory synapse loss. The ketamine analogue grants faultless
activity-guided regrowth, ignoring maladaptive sprouting; the SSRI
routine sidesteps debates over serotonin depletion after long exposure
\[13\]; the neurosteroid module dampens every hidden unit equally,
whereas real extrasynaptic GABA_A receptors sit on select neurons.

Inter-seed variance arises from random data splits and weight
initialisation, not from modelled genetic or hormonal modifiers.
Maintenance schedules are sketched loosely on clinical practice---brief
boosters for ketamine, longer courses for the others---but do not
address dose, tolerability, or adherence. Adding recurrent dynamics,
cell-type specificity, and empirically derived patient heterogeneity
will be essential next steps.

### Conclusion

Within these constraints, the simulations offer a coherent narrative:
fragile circuits can be helped in three distinct ways---rebuilding lost
links, patiently tuning what remains, or providing a temporary brake on
over-excitation---but only the first delivers uniform, lasting
protection against future stress. A single framework that recreates
these divergent trajectories narrows the gap between computational
theory and bedside choice, supporting a shift toward mechanism-guided,
plasticity-focused care as rapid-acting agents become mainstream \[12\].

## References

\[1\] World Health Organization. (2022). World mental health report:
Transforming mental health for all. World Health Organization.

\[2\] Rush, A. J., Trivedi, M. H., Wisniewski, S. R., et al. (2006).
Acute and longer-term outcomes in depressed outpatients requiring one or
several treatment steps: A STAR\*D report. American Journal of
Psychiatry, 163(11), 1905-1917.
https://doi.org/10.1176/ajp.2006.163.11.1905

\[3\] Trivedi, M. H., Rush, A. J., Wisniewski, S. R., et al. (2006).
Evaluation of outcomes with citalopram for depression using
measurement-based care in STAR\*D: Implications for clinical practice.
American Journal of Psychiatry, 163(1), 28-40.
https://doi.org/10.1176/appi.ajp.163.1.28

\[4\] Murrough, J. W., Iosifescu, D. V., Chang, L. C., et al. (2013).
Antidepressant efficacy of ketamine in treatment-resistant major
depression: A two-site randomized controlled trial. American Journal of
Psychiatry, 170(10), 1134--1142.
https://doi.org/10.1176/appi.ajp.2013.13030392

\[5\] Iadarola, N. D., Niciu, M. J., Richards, E. M., et al. (2015).
Ketamine and other NMDA receptor antagonists in the treatment of
depression: A perspective review. Therapeutic Advances in Chronic
Disease, 6(3), 97-114. https://doi.org/10.1177/2040622315579059

\[6\] Gunduz‑Bruce, H., Takahashi, K., et al. (2022). Development of
neuroactive steroids for the treatment of postpartum depression. Journal
of neuroendocrinology, 34(2), e13019.

\[7\] Duman, R. S., & Aghajanian, G. K. (2012). Synaptic dysfunction in
depression: Potential therapeutic targets. Science, 338(6103), 68-72.
https://doi.org/10.1126/science.1222939

\[8\] Cheung, N. (2026). Divergent Mechanisms of Antidepressant
Efficacy: A Unified Computational Comparison of Synaptogenesis,
Stabilization, and Tonic Inhibition in a Model of Depression. Zenodo.
https://doi.org/10.5281/zenodo.18290014

\[9\] Stahl, S. M. (1998). Mechanism of action of serotonin selective
re-uptake inhibitors: Serotonin receptors and pathways mediate
therapeutic effects and side effects. Journal of Affective Disorders,
51(3), 215--235. https://doi.org/10.1016/S0165-0327(98)00221-3

\[10\] Boschloo, L., Hieronymus, F., Lisinski, A., et al. (2023). The
complex clinical response to selective serotonin reuptake inhibitors in
depression: a network perspective. Translational Psychiatry, 13(1), 19.

\[11\] Page, C. E., Epperson, C. N., Novick, A. M., et al. (2024).
Beyond the serotonin deficit hypothesis: communicating a neuroplasticity
framework of major depressive disorder. Molecular psychiatry, 29(12),
3802--3813. https://doi.org/10.1038/s41380-024-02625-2

\[12\] Krystal, J. H., Abdallah, C. G., Sanacora, G., et al. (2019).
Ketamine: A paradigm shift for depression research and treatment.
Neuron, 101(5), 774--778. https://doi.org/10.1016/j.neuron.2019.02.005

\[13\] Moncrieff, J., Cooper, R. E., Stockmann, T., et al. (2023). The
serotonin theory of depression: A systematic umbrella review of the
evidence. Molecular Psychiatry, 28(8), 3243--3256.
https://doi.org/10.1038/s41380-022-01661-0
