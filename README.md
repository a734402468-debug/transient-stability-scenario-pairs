# Transient stability scenario pairs

Case data for a study of how to construct a synchronous or out-of-step counterpart to a specified operating point while preserving the conditions of the comparison. The release contains the operating-point results, selected rotor responses and direction-selection counts reported in the paper. Its scope is limited to case data, with no guarantee of independent reproduction of the simulations.

| Study | Comparison | Data and figures |
|---|---|---|
| 118-bus system | Retain the synchronous point and construct an out-of-step counterpart at matched export and generator voltage setpoints. | [Operating points](118-bus/operating-points.csv) · [Two-step classifications and event times](118-bus/classification.csv) · [Rotor response (PDF)](118-bus/rotor-response.pdf) |
| Southern Xinjiang | Retain the out-of-step point and construct synchronous counterparts under progressively stricter plant schedule holds. | [Plant holds](southern-xinjiang/plant-holds.csv) · [Three-plant-hold redispatch](southern-xinjiang/H3-redispatch.csv) · [Plotted angle data](southern-xinjiang/H3-rotor-response.csv) · [Redispatch and rotor response (PDF)](southern-xinjiang/redispatch-and-response.pdf) |
| Additional operating backgrounds | Construct counterparts at two further load levels per model, with and without a plant schedule hold. | [Reference qualification and task outcomes](operating-backgrounds.csv) |
| Fault clearing time | Reassess the two original dispatch pairs with clearing one local grid cycle earlier or later. | [Endpoint classes and first sustained slip at both time steps](clearing-time-sensitivity.csv) |
| Direction-selector ablation | Change the selector while keeping the four candidate directions and the physical acceptance procedure fixed within each task. | [Decision counts by task and selector](selector-ablation/results.csv) |

### 118-bus system

The actual interface export is the signed sum of AC flows on 20 branches. Both points satisfy the 757.054663 ± 1 MW target. Their exports are 756.262691 and 757.038943 MW, respectively, and all 47 generator voltage setpoints match. Schedule changes in the CSV are measured from the common starting dispatch. The 5 and 2.5 ms simulations confirmed both classes over the 20 s post-clearance window. Angle displacement is positive when G69 advances relative to G76. Empty event-time and event-angle fields mean that the corresponding event was not observed.

### Southern Xinjiang

H0 allows all eligible compensating plants. H1 holds Aert at its reference active-power schedule, H2 also holds Yonga, and H3 adds Shenk. Each hold uses the plant-wide schedule readback and a tolerance of ±0.0001 MW. All five rows of the plant-hold table are synchronous over the 10 s post-clearance window at both 2.5 and 1.25 ms. The strictest admissible hold level depends on which plant supplied the compensating increase.

For H3, `single` and `split` identify the two qualifying compensation patterns in both CSVs. The angle series give Dake's displacement relative to the external grid from its prefault value in each 2.5 ms run. Times are measured from simulation start. The CSV retains the recorded sample order, including repeated timestamps.

### Direction-selector ablation

Each language-model configuration received 20 requests per task, with each candidate appearing five times at each display position. The deterministic rule made one decision per task. A valid selection identifies an allowed direction. A selection yielding the required pair also satisfies the study's operating and dynamic requirements. The last column counts distinct qualifying dispatches within each row. Repeated selections of a dispatch use the same physical evidence.

Astra and Sol used high reasoning effort, JSON output and a 4096-token output limit. The two official DeepSeek configurations used JSON output and the same shared 4096-token limit, with high or low reasoning effort. Qwen used separate allowances of 3584 reasoning tokens and 512 answer tokens with application-side JSON validation. The decision counts include truncated and malformed answers.

### Additional operating backgrounds

`operating-backgrounds.csv` gives four prespecified backgrounds. R0 uses the basic permissions. R1 adds one plant schedule hold. Its two columns distinguish exclusion before direction generation from screening after generation. The 118-bus lower-load reference violated six static limits. The reported G65 violation is shown for each 118-bus background; candidate evaluation did not start in either. An empty cell means the value is inapplicable or unreported. Southern Xinjiang uses aggregate plant MW. At each load the first proposal used Dake and Shenk_FE and satisfied the Aert_PHS hold. The hold changed the fourth direction from one with Aert_PHS to one with huaw_FE; that direction was not simulated. Each of the six qualified paths had a logical cost of 6 AC evaluations and 2 RMS simulations. They share two sets of background-specific physical evidence. The scheduled inputs had occurred previously; the two new backgrounds underwent separate physical evaluation.

### Fault clearing time

`clearing-time-sensitivity.csv` gives the reported results at the original time step and half step for each endpoint. Fault duration runs from inception to clearance. Slip times are seconds from simulation start and refer to the first rotor pair satisfying the sustained-slip criterion. Blank slip times indicate that the criterion was not met within the observation window. At the original clearing time, the endpoint classifications and times come from archived evidence. The eight endpoint evaluations at the four shifted conditions used 16 new RMS runs. The Southern Xinjiang counterpart in this experiment uses the H3 single-plant allocation (huaw_FE). The separate load-background experiment uses Shenk_FE.

These two additions transcribe the reported case results. Across both experiments, 56 AC evaluations (including 15 final restoration power flows) and 24 RMS simulations were newly run. All 15 dispatched work items passed restoration checks.
