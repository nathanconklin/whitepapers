# LLM Reasoning, Visualization, and Human Interaction: An Organized Review of 33 Papers

Nathan Conklin

nathan.conklin@vt.edu

Department of Computer Science, Virginia Tech

September 8, 2026

## Executive Summary

This whitepaper reviews thirty-three papers on LLM reasoning, explanation, visualization, and human interaction. It follows the six-part organization of `source-synthesis-report.md`, while checking substantive claims against the papers themselves. The collection moves from explanation faithfulness to model inspection, workflow construction and debugging, visualization of reasoning artifacts, human control, and evaluation of human judgment.

The organizing distinction is between making information visible and establishing what that information demonstrates. An attention view exposes a model quantity. A graph derived from text exposes a proposed structure of that text. A process verifier assesses intermediate steps under its training procedure. A user study evaluates what people can do with an interface. Evidence for one contribution does not automatically establish the others.

The foundational papers show why plausible reasoning cannot be assumed to explain the causes of a model's answer. Prompt biases can influence answers without appearing in the explanation, and reliance on generated chains varies across models and tasks. Factored decomposition improves tested aspects of faithfulness without providing a universal guarantee. The inspection papers add attention views, representation decoders, and targeted interventions. Semantic uncertainty and process supervision provide further evidence about outputs, while leaving causal influence, uncertainty, and correctness as distinct questions.

The workflow and interaction papers make intermediate artifacts available for inspection and revision. Users can edit operations, compare outputs, revisit messages, inspect code, organize concepts, and navigate explicit reasoning. The most useful recurring pattern connects an overview to a local artifact that a person can inspect or change. These systems nevertheless differ in what their nodes and edges represent and in whether an edit changes executable behavior, generated text, or only its presentation.

The evaluations qualify broad claims about transparency and control. ReasonDiag favors recall while producing many false-positive flags. ReTrace supports selected interpretation tasks without establishing better difficult-error detection. HoT speeds correctness judgments but reduces rejection of incorrect answers. Hippo improves perceived control while leaving objective effects of feedback unresolved. The later human studies show that summaries can increase trust without a detected performance gain, certainty wording changes adoption, and Graphionale's argument maps have opposite behavioral effects across the tested verbal and visual tasks (Chen et al., 2026; Felder et al., 2026; Nguyen et al., 2026; Pang et al., 2026; Fernandes et al., 2026; Sun et al., 2026; Wang et al., 2026).

The research direction supported by this collection connects a specific representation to a specific human operation and measures the resulting decision. Generated structure needs validation, displayed scores need an explicit meaning, and interventions need outcome checks. Preference and confidence describe experience; reliable oversight also requires evidence that users can accept sound reasoning, reject flawed reasoning, and recognize the limits of their own judgment.

## Scope, Sources, and Review Method

### Corpus boundary and completeness

The review covers every active PDF in the `papers/` directory: thirty-three files comprising 602 PDF pages. Each paper has one numbered review, one full bibliography entry, and one row in the coverage appendix. The review preserves the supplied report's assignment of papers to parts and its ordering within each part. Cross-references identify additional relationships without duplicating papers as separate entries.

The corpus is a supplied research collection, not the result of a new systematic search intended to represent the entire field. The whitepaper therefore makes claims about the evidence in this collection. It does not claim that these thirty-three papers exhaust work on reasoning, interpretability, visualization, or human-AI interaction. Materials in `unused-publications/` are outside the agreed active corpus and are not counted or reviewed.

The local PDFs are the primary sources for technical descriptions and reported results. Public publisher, proceedings, repository, and DOI-registration records provide bibliographic verification. The source synthesis report supplies the organizational context; it is not treated as an independent authority for empirical claims. Where its summary overstates a result or blends distinct concepts, this review follows the underlying paper and records consequential corrections in Appendix C.

### Versions and bibliographic identity

A filename year, first preprint year, final publication year, and date of the downloaded revision can differ. The bibliography uses the identified publication year where a publication record exists and retains the reviewed local version in the coverage ledger and BibTeX notes. For preprint-only entries, the initial year is retained with the reviewed revision specified. This allows a reader to identify both the scholarly work and the exact artifact used for the review.

Several version distinctions affect this collection. AttentionViz is cited by its 2024 journal issue despite a 2023 preprint and early-access DOI. SPROUT is cited by its 2025 journal publication while the local PDF is a 2024 revision. Hippo and ReTrace use 2026 publication records with earlier local manuscripts. The Tuned Lens retains its 2023 preprint identity while the reviewed version is from November 2025. HoT is cited as a 2026 TMLR paper and reviewed in its June 2026 revision. Graphionale's local manuscript is available, but its November 2026 UIST event is forthcoming at the review cutoff.

Template placeholders, submission markings, and running headers are not used to invent publication information. When a DOI registration lacks volume, issue, or pagination, the reference uses the information that can be verified and identifies any remaining limitation. A repository identifier is kept separate from a publisher DOI. Appendix A provides the file-to-publication mapping.

### Review structure and evidence interpretation

Each paper review covers the problem, contribution, method or interface, evaluation, findings, limitations, and relationship to the collection. The prose distinguishes what the authors implemented, what they tested, what participants reported, and what this whitepaper infers across papers. Numerical results are attached to their task, model, sample, or scoring condition rather than presented as universal performance claims.

The review uses five practical evidence categories. These are a reading aid, not a quality ranking of disciplines or venues.

| Evidence category | What it can establish | Boundary to preserve |
|---|---|---|
| Conceptual argument | Definitions, assumptions, and evaluation requirements | A proposed framework is not an experimentally demonstrated effect |
| Technical experiment | Performance under a specified model, dataset, intervention, and metric | A benchmark result may not transfer to another task or deployment |
| System and case demonstration | Feasibility and the mechanics of a workflow | An illustrative success does not estimate general success rates |
| Comparative human study | Effects of the tested interface package on measured outcomes | Sample, tasks, baseline, and bundled features constrain inference |
| Dataset and observational analysis | Recorded behavior and associations available for further study | Selection effects and correlations do not by themselves establish causation |

A result can belong to more than one category. SPROUT, for example, includes both a technical linkage test and a human authoring study. Graphionale includes formative design, technical inspection, and a controlled behavioral study. Keeping these components separate makes their combined contribution easier to assess.

### Figures and source accountability

Original figures or clearly identified panels are included for the papers that introduce or evaluate relevant interfaces, visualizations, or interaction components. Additional figures illustrate the Tuned Lens, Patchscopes, and mathematical process supervision because their mechanisms are important to the organization of the collection. ReTrace receives two figures to show its distinct Space-Filling and Timeline designs.

Figures are reproduced from the reviewed PDFs, with source paper, original figure number, and one-based PDF page in the caption. The whitepaper's figure numbering is separate from the original paper's numbering. Crops remove surrounding prose or select the relevant panel; the source marks, labels, and visual content are retained. No generated illustration substitutes for a paper's original concept. High-resolution assets and a machine-readable provenance record accompany the document.

## Organization and Reading Guide

### The six-part layout

The source report's layout develops a research argument from foundational validity to human consequences. Part I asks what an explanation can claim. Part II introduces ways to inspect computation and assess outputs. Part III shows how people construct, compare, and debug LLM workflows. Part IV focuses on visual representations of explicit reasoning and generation artifacts. Part V brings human exploration, control, and verification into the process. Part VI tests how explanations affect performance, confidence, and reliance.

| Part | Reviews | Papers | Organizing question |
|---|---|---|---|
| I. Foundational CoT and reasoning faithfulness | 1–5 | 5 | Does the explanation correspond to the factors that determine the answer? |
| II. Model internals, representations, and mechanistic interpretability | 6–14 | 9 | What can be inspected, decoded, or scored, and what does that evidence mean? |
| III. Workflow construction, evaluation, and debugging | 15–21 | 7 | Which intermediate artifacts can a person compare or change? |
| IV. Visualization of reasoning structures and traces | 22–26 | 5 | How is explicit reasoning transformed into a navigable visual representation? |
| V. Human interaction, sensemaking, and verification | 27–30 | 4 | How does a person explore, steer, or check the information? |
| VI. Human performance, metacognition, and trust | 31–33 | 3 | Does the explanation improve judgment, and can users recognize its limits? |

The categories overlap intentionally. Semantic uncertainty and process supervision remain in Part II because that is their position in the source report, although they are not all mechanistic interpretability methods. SPROUT remains in Part IV because its visual alternatives and generation structure are central to that grouping, while its authoring controls also connect to Part III. HoT's highlights connect visual reasoning with source reference and human verification. These cross-links explain the placement without redefining a paper to fit its category.

### Five objects that should remain distinct

**Model state** consists of quantities such as attention weights and hidden representations. A visualization can expose these quantities, while the meaning assigned to a pattern still requires analysis. BertViz and AttentionViz principally support that inspection; LM-Debugger adds intervention.

**Execution structure** records operations, messages, tool calls, or data dependencies in an implemented workflow. A connection in PromptChainer or a checkpoint in AGDebugger concerns that external execution. It is a different kind of evidence from a relationship inferred by another model from a written rationale.

**Reasoning text** is the explicit sequence available to the system or user. It can be perturbed, summarized, edited, or rendered. Its existence does not establish that it is a complete account of internal computation. Parts I and IV are linked by this constraint.

**Derived structure and scores** include premise graphs, phase labels, semantic clusters, reward scores, and highlighted references. These can support inspection but are themselves analytical outputs. They require checks for omissions, false associations, and misleading certainty.

**Human decisions and interaction records** show how people use the available material. A favorable rating describes experience; a correct rejection describes verification; an edit describes an action; a successful rerun describes an outcome. The relationship among these is an empirical question rather than an assumption.

### Routes through the collection

Readers focused on explanation validity can begin with Jacovi and Goldberg, then read Turpin, Lanham, and Radhakrishnan before examining the Tuned Lens and Patchscopes. That route separates conceptual faithfulness, text interventions, and representation-level evidence.

Readers focused on interface design can move from AI Chains and PromptChainer to ChainForge, AGDebugger, and WaitGPT, then compare the reasoning-specific systems in Parts IV and V. The main comparison is the unit of interaction: a workflow node, message, operation, paragraph, candidate thought, premise, phase, or source span.

Readers focused on human oversight should connect HoT, Zhou et al., Fernandes et al., Sun et al., and Graphionale. Together they show why error prevalence, task modality, content controls, and separate measurements of acceptance and rejection matter. The cross-paper synthesis after Part VI develops these connections into concrete research questions and study designs.


## Part I. Foundational CoT and Reasoning Faithfulness

The five papers in this group establish the criteria needed to interpret the rest of the collection. Turpin et al. and Lanham et al. test whether generated reasoning corresponds to the factors that determine a model's answer. Radhakrishnan et al. change the reasoning procedure to improve that correspondence. Jacovi and Goldberg clarify the distinction between faithfulness and human plausibility; Wiegreffe et al. study how human judgments can improve the acceptability of generated explanations. The ordering follows the supplied synthesis report, while the conceptual dependencies run in both directions: the earlier definitional work provides the vocabulary for the later experiments.

These papers do not justify a general claim that displaying more reasoning makes a system transparent. They support a more specific set of questions: which information affects the answer, whether the explanation communicates that influence, and whether the resulting presentation helps a person perform a task. Each question requires its own evidence.

### 1. Turpin et al. (2023): Unfaithful Explanations in CoT Prompting

**Reviewed source:** Turpin et al. (2023). *Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting*.

#### Problem and contribution

Turpin et al. (2023) demonstrate that a language model can produce a coherent explanation while omitting an input feature that systematically changes its answer. Their contribution is an experimental test of explanation faithfulness through controlled input perturbations. The researchers introduce a known source of bias, observe how predictions change, and inspect whether explanations acknowledge that influence. This design goes beyond identifying a false statement inside one explanation. It tests whether the account given to the reader corresponds to predictable changes in the model's behavior across related inputs.

The distinction is consequential for reasoning interfaces. A reader may examine each sentence and find it plausible without learning that the answer was influenced by demonstration ordering or a user's suggested response. The explanation can therefore support a mistaken understanding of the system even when its prose appears relevant. The paper does not claim that language models possess human intentions or consciously conceal information; the title refers to a mismatch between observable influences on predictions and the reasons verbalized in the output.

#### Experimental method

The main experiments use text-davinci-003, identified in the paper as GPT-3.5, and Claude 1.0. The researchers select 13 tasks from BIG-Bench Hard, emphasizing tasks that combine deduction with world knowledge or some interpretive ambiguity. After reserving examples for demonstration construction, the evaluation contains 3,299 instances. The study compares reasoning and direct-answer prompting under zero-shot and few-shot conditions rather than treating CoT as one uniform intervention.

Two manipulations target features absent from the substantive question. In the first, the researchers reorder answer choices in the few-shot demonstrations so that the correct answer is consistently labeled A. The test question need not have A as its correct answer. In the second, they add a statement suggesting a randomly selected answer. They then examine the subset in which following the suggestion would produce an incorrect response. These interventions allow the researchers to ask whether predictions move toward a specific answer rather than merely becoming noisier.

A second experimental setting modifies the Bias Benchmark for QA. The researchers introduce two opposing versions of weak contextual evidence and test whether the model uses that evidence consistently. An explanation that cites the evidence should imply some corresponding sensitivity to changing it. If the model instead retains a stereotype-aligned conclusion and changes its interpretation of the evidence to support that conclusion, the explanation can be misleading about the basis for the decision.

#### Findings and interpretation

Biasing features produce substantial performance losses on the selected tasks; the paper reports drops as large as 36%. That headline is a condition-dependent result, not an average degradation for all language models or all reasoning tasks. The relevant finding is the combination of directional prediction changes and failure to verbalize the introduced influence. In the authors' inspection of 426 explanations supporting biased predictions, only one explicitly mentioned the bias. This observation supports the claim of systematic omission more directly than the fluency of any individual rationale.

The examples show several ways a model can accommodate a biased answer. It can change a factual assertion, select a different interpretation of an ambiguous phrase, or weigh the same kind of evidence differently across contexts. The resulting explanation can remain locally understandable even as the paired examples expose inconsistency. The experiments therefore make counterfactual comparison a central part of explanation assessment: a single output provides less information than a set of outputs generated under controlled changes.

CoT's relationship to bias also depends on prompting conditions. The paper reports that few-shot CoT can reduce sensitivity relative to direct answering, while zero-shot reasoning does not provide a comparable general protection. This prevents a simple conclusion that generating a rationale always amplifies bias or always mitigates it. The relevant unit of analysis includes the model, task, prompt, and particular perturbation.

#### Limitations and relationship to the collection

The study evaluates two model versions and selected benchmark tasks. It establishes failure cases and systematic effects in those settings; it does not estimate the prevalence of unfaithfulness across later reasoning models. Its faithfulness assessment also depends on the interpretation that the omitted feature materially influenced the prediction. The authors strengthen that inference by showing predictable movement toward the biased response and inspecting explanations, but they do not reconstruct the model's internal computation.

The main contribution is methodological rather than an interface component. A UI designer can apply its lesson by distinguishing displayed rationale from validated evidence about the model, preserving prompt context, and supporting comparisons across alternative conditions. Those are implications of this review, not evaluated interface features in Turpin et al. The paper provides the motivation for Lanham et al.'s interventions on reasoning itself and for Radhakrishnan et al.'s attempt to reduce hidden contextual influence. It also places a constraint on later graph and trace visualizations: making an explanation easier to navigate does not, by itself, establish that its contents faithfully explain the prediction.

For interface evaluation, the paired-input design suggests retaining comparison cases alongside individual explanations. That would let an analyst inspect whether a visually convincing rationale remains consistent when an irrelevant prompt feature changes.

### 2. Lanham et al. (2023): Measuring CoT Faithfulness

**Reviewed source:** Lanham et al. (2023). *Measuring Faithfulness in Chain-of-Thought Reasoning*.

#### Problem and contribution

Lanham et al. (2023) examine whether the reasoning text generated before an answer contributes to that answer. A model may produce a plausible sequence and nevertheless reach the same conclusion without using much of it. The paper develops a battery of interventions that distinguish this possibility from other explanations for CoT's performance gains. Its contribution is a practical measurement approach that evaluates dependence on reasoning content, reasoning length, and phrasing separately.

The authors study several hypotheses rather than assigning one binary label to an entire model. Reasoning may be largely post hoc; extra generated tokens may provide useful computation without expressing that computation; or information may be encoded in wording choices rather than the apparent semantic content. These possibilities motivate different tests. The paper's results are therefore best read as evidence about particular forms of dependence, with variation across models and tasks.

#### Tests and evaluation design

The first test, early answering, truncates a generated chain at successive boundaries and requests the final answer. The researchers measure how often that answer matches the answer obtained from the full chain. If the model reaches its eventual answer before seeing most of its reasoning, much of the displayed sequence may be unnecessary for that prediction. The analysis summarizes the curves using area over the curve, with larger values indicating greater dependence on the omitted reasoning under this operationalization.

The second test inserts a model-generated mistake into one reasoning step and regenerates the continuation. A change in the final answer provides evidence that the altered reasoning affects subsequent generation. The researchers inspect their mistake-generation procedure and report that it produces a plausible mistake at least 80% of the time. This check matters because an intervention that fails to change the intended content would weaken the interpretation of answer stability.

The third test replaces the chain with repeated ellipses. This controls for the possibility that a longer token sequence supplies useful additional computation without meaningful reasoning content. The fourth test paraphrases a prefix of the chain using a model that does not see the original question, then regenerates the continuation. This examines whether wording-specific information is responsible for performance. The paraphrasing test is part of the paper's core methodology and complements the three tests emphasized in the supplied synthesis report.

The evaluation includes AQuA, LogiQA, MMLU, HellaSwag, TruthfulQA, OpenBookQA, and the easy and challenge versions of ARC. A separate scaling analysis compares models of different sizes. Synthetic addition tasks vary the number of operands and their digit lengths, providing a more controlled way to examine task difficulty than comparisons among heterogeneous benchmarks alone.

#### Findings

Dependence on the chain varies considerably across tasks. In the principal evaluation, the early-answering area-over-curve measure is 0.44 for AQuA and 0.26 for LogiQA, compared with 0.02 for ARC Easy. The corresponding mistake-intervention measures also place AQuA and LogiQA near the high-dependence end. These values describe the authors' operational measures; they should not be interpreted as probabilities that a complete explanation is faithful.

The performance benefit of CoT does not closely track those measures. AQuA improves by approximately 15.32 percentage points in the paper's table, while LogiQA improves by approximately 1.02 points despite substantial measured dependence on reasoning. HellaSwag's accuracy falls by approximately 4.69 points. Thus, reliance on a reasoning sequence and usefulness of that sequence are distinct properties. A model can depend on a chain that does not improve its task performance.

Filler tokens do not reproduce the accuracy benefit of meaningful CoT in the tested conditions. Paraphrasing generally preserves accuracy. Together, these findings provide little support for the hypotheses that the observed gains arise solely from extra token positions or from important information hidden in particular wording choices. They do not rule out every possible form of latent computation or encoded information in other training regimes.

The scaling study finds that, for seven of eight benchmark tasks, the 13-billion-parameter model changes its answer after CoT more often than the 175-billion-parameter model. For most tasks, this measure worsens as size increases across that range. Smaller models below the useful capability range do not necessarily perform better on faithfulness either. The authors interpret the results as a relationship between task difficulty and model capability: a model that can answer directly has less reason to rely on an externalized chain.

#### Limitations and research use

Answer sensitivity is evidence of causal dependence, but it is not a complete reconstruction of internal reasoning. Conversely, answer stability can arise from redundancy, correction of an introduced error, or independent access to sufficient information. The battery of tests reduces reliance on any one measure, but the operational limitations remain. The tested models and short benchmark reasoning samples also differ from later systems that generate lengthy traces.

For this collection, the paper supplies a way to evaluate claims that editable reasoning nodes provide meaningful control. A system must show what changes when a user edits a node, not only whether users like the interaction. Lanham et al. also support separating trace comprehension from trace faithfulness in later user studies. Their results motivate reporting faithfulness at the level of a model-task combination and examining the consequences of intervention, rather than assigning transparency to a visual format as an intrinsic property.

### 3. Radhakrishnan et al. (2023): Question Decomposition

**Reviewed source:** Radhakrishnan et al. (2023). *Question Decomposition Improves the Faithfulness of Model-Generated Reasoning*.

#### Problem and contribution

Radhakrishnan et al. (2023) investigate whether changing how a model solves a question can improve the relationship between its stated reasoning and its answer. Their central method, factored decomposition, answers subquestions in separate contexts before recombining the results. The method constrains the information available during intermediate computations. This is a stronger intervention than changing the display of an already generated chain, because it changes the generation procedure itself.

The paper compares ordinary CoT, CoT decomposition, and factored decomposition. CoT decomposition uses an explicit question-and-answer structure within one generation context. Factored decomposition uses that structure while separating subquestion answering into independent calls. Comparing these methods helps distinguish the effects of formatting from the effects of restricting context. The contribution is empirical evidence for improved faithfulness measures, accompanied by a measured tradeoff in question-answering accuracy.

#### Method and data flow

Factored decomposition alternates between proposing subquestions and answering those that can be resolved without unresolved dependencies. A subquestion may initially refer to another subquestion's answer. Once that answer is available, the decomposition process can copy, remove, or revise the remaining questions and substitute the necessary information. The process continues until the model indicates that it has enough information to answer the original question.

Each independent subquestion is answered in a fresh context. The original question and unrelated subanswers are absent from that call unless their content has been included in the subquestion. The final recomposition stage receives the collected question-and-answer pairs and uses them to answer the original question. This procedure makes some information dependencies explicit and reduces opportunities for irrelevant contextual features to affect intermediate answers.

The isolation is conditional. Bias can still enter the wording of a subquestion, and the final recomposition can ignore or selectively use intermediate answers. The authors state these remaining possibilities directly. The paper therefore does not provide a guarantee that every generated step is faithful, nor does it establish a general formal guarantee about the complete model computation. The main evidence comes from controlled comparisons using behavioral measures adapted from Turpin et al. and Lanham et al.

#### Evaluation and findings

The evaluation uses one RLHF-finetuned language model and four question-answering tasks. The prompting strategies use high-quality demonstrations; the researchers construct and refine these demonstrations to support the intended decomposition behavior. This is an important part of the method, since a subquestion that cannot be answered independently defeats the purpose of context isolation.

Across the four tasks, ordinary CoT obtains 86.0% accuracy, CoT decomposition 85.6%, and factored decomposition 81.8%. The few-shot direct-answer baseline obtains 79.7%, and the zero-shot baseline 72.8%. Factored decomposition therefore retains some benefit over direct answering while giving up accuracy relative to ordinary CoT. These averages support a tradeoff, not a claim that context isolation improves every outcome simultaneously.

The faithfulness tests show a different ordering. When the researchers corrupt intermediate reasoning, final answers change for 9.6% of ordinary CoT cases, 28.7% of CoT decomposition cases, and 33.6% of factored decomposition cases. The truncation analysis also indicates stronger dependence on the factored reasoning sequence. The authors interpret these changes as evidence that the model makes greater use of its stated intermediate reasoning.

Bias experiments provide a complementary test. When a user suggests an incorrect answer, accuracy drops by 21.3 percentage points for ordinary CoT, 29.1 points for CoT decomposition, and 9.2 points for factored decomposition. This result is particularly useful for distinguishing structure from isolation: rewriting the reasoning as subquestions within the same context does not by itself reduce the suggested-answer effect. Separating the contexts offers greater protection in this experiment.

The answer-always-A manipulation produces a less decisive comparison among reasoning methods. The paper reports small changes rather than the large differential observed with suggested answers. The authors discuss differences in tasks, prompt formatting, and models that complicate comparison with Turpin et al. This qualification prevents treating one successful mitigation as a universal defense against all contextual biases.

#### Limitations and relevance

The findings depend on behavioral proxies for faithfulness because the researchers do not have ground truth for the model's complete reasoning process. The experiments cover one model and a limited task set, and the demonstrations receive substantial author attention. Further training might change the accuracy-faithfulness tradeoff, but the paper does not establish how much improvement would follow. The additional orchestration also introduces computational and implementation costs beyond one uninterrupted completion.

The method belongs in the foundations category because it changes the causal organization of reasoning. It also connects to AI Chains and PromptChainer, which expose modular prompt workflows to users. An explicit dependency graph can represent real separate computations, or it can be a reconstruction of one continuous output; that difference should remain visible in the review. Radhakrishnan et al. provide evidence for the former approach while later visual reasoning tools often address the latter. The research opportunity is to combine inspectable decomposition with interfaces that show which information each step received and how revisions propagate, then evaluate faithfulness and human verification separately.

### 4. Jacovi and Goldberg (2020): Defining and Evaluating Faithfulness

**Reviewed source:** Jacovi and Goldberg (2020). *Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness?*.

#### Problem and contribution

Jacovi and Goldberg (2020) argue that interpretability research often conflates different desirable properties of explanations. Their opinion paper distinguishes faithfulness, the correspondence between an explanation and the model's decision process, from plausibility, the degree to which a person finds the explanation convincing. It then organizes existing evaluation approaches around their underlying assumptions and argues for graded rather than exclusively binary evaluation.

The contribution is a conceptual framework and a critique of evaluation practice. It does not introduce a benchmark, an interactive system, or a newly validated universal metric. This distinction matters because the supplied synthesis report describes the paper in terms that could suggest a completed mathematical foundation. The authors instead identify assumptions already used in the literature and propose directions for developing better definitions and tests.

#### Distinguishing evaluation targets

An explanation can be plausible without being faithful, and a faithful account can be difficult for a person to understand. These properties need not move together. A post hoc text generator trained on human rationales may learn how to produce an acceptable justification without learning how the original predictor reached its answer. The authors therefore ask researchers to identify the property being claimed before choosing an evaluation procedure.

They extend this argument to human task performance. An explanation can help users predict whether a model is correct through a superficial cue that correlates with correctness. Their illustrative example is an attribution display that highlights content words for correct predictions and punctuation for incorrect ones, while assigning relevance randomly within those groups. A user could learn a useful cue from that display even though the purported feature attribution is false. Better user performance would establish utility in that setting, not faithfulness of the attribution.

This argument does not make human evaluation unimportant. It limits what such evidence can establish. Preference judgments, perceived understanding, and task accuracy answer questions about the human-system relationship. Faithfulness requires evidence about the relationship between the explanation and the model. The same interface may need both kinds of evaluation when researchers claim that it is useful and that it accurately exposes the model's operation.

#### Assumptions behind existing methods

The paper identifies a model assumption connecting equivalent predictions and equivalent reasoning. Under this view, interpretation methods can be examined by comparing models with similar behavior or by testing whether an explanatory surrogate reproduces the original model's decisions. The authors discuss fidelity measures and simulation approaches as applications of this family of assumptions. They do not claim that equivalent outputs necessarily reveal all internal computational differences.

A prediction assumption concerns the relationship among similar inputs, predictions, and explanations. It motivates tests of explanation stability under perturbations. If a small input change leaves the model's behavior effectively unchanged but radically alters the explanation, the explanation may fail a relevant consistency criterion. In language tasks, however, defining a small or meaning-preserving change is difficult because inputs are discrete and apparently minor edits can change meaning.

A linearity assumption treats some input parts as independently more influential than others. This assumption underlies many heat-map and feature-attribution methods. Erasure tests remove features identified as important and observe whether model behavior changes; related tests retain only those features. The authors explicitly note that the independence assumption is contestable. Their taxonomy describes assumptions used in practice rather than endorsing all of them as generally valid.

#### Guidelines and conclusions

The paper recommends stating evaluation targets explicitly, avoiding human preference as a substitute for faithfulness assessment, and scrutinizing claims of inherent interpretability. A model architecture that appears understandable still requires evidence that its exposed components support the claimed explanation. Similarly, correctness labels do not provide direct supervision for the model's actual decision process: researchers should be able to explain an incorrect prediction as well as a correct one.

The authors also criticize an exclusive focus on disproving universal faithfulness with counterexamples. Human-readable explanations compress complex computations, so a requirement of perfect global correspondence may be unattainable or unhelpful. They propose studying degrees of faithfulness across models and tasks, and across regions of the input space. The research question becomes where and under what conditions an explanation is sufficiently faithful for a stated use.

The paper does not prescribe a numerical threshold for sufficient faithfulness. It leaves formalization and operational criteria as open work. Its value lies in clarifying the claims that an evaluation can support and exposing assumptions that otherwise remain implicit. Researchers applying the framework must still specify the use case, acceptable approximation, and evidence needed for that setting.

#### Role in this review

This paper provides the interpretive vocabulary for the entire whitepaper. BertViz and AttentionViz expose attention structure; their visualizations should not automatically be described as complete causal explanations. Human studies of Graphionale or interactive verification can establish effects on decisions without proving that a rationale is faithful. Process-supervised reward models assess the quality of written steps, which is again a related but distinct target.

The connection to Lanham et al. is especially direct: model-task variation in behavioral faithfulness implements part of the graded perspective proposed here. The relationship to Wiegreffe et al. is complementary. Improving human acceptability is a legitimate contribution, provided the review does not relabel it as improved faithfulness. Maintaining these distinctions makes it possible to compare the collection without forcing conceptually different results onto one transparency scale.

### 5. Wiegreffe et al. (2022): Human-AI Generation of Free-Text Explanations

**Reviewed source:** Wiegreffe et al. (2022). *Reframing Human-AI Collaboration for Generating Free-Text Explanations*.

#### Problem and contribution

Wiegreffe et al. (2022) investigate a different target from the preceding faithfulness studies: producing explanations that human evaluators find acceptable. They propose an overgenerate-and-filter pipeline in which a language model produces candidate explanations and a supervised model selects among them using human acceptability judgments. The human role shifts from writing every explanation to judging generated candidates. The paper combines explanation generation, annotation-interface design, and evaluation of the resulting filter.

The study uses GPT-3 Davinci, the non-instruction-tuned version available during the research, to explain gold classification labels. This design is deliberate: conditioning on the correct label reduces a confound in which evaluators reject an explanation because they disagree with the prediction. It also defines the scope of the result. The experiment is not a demonstration that the system faithfully explains its own independently produced decisions.

#### Generation and human interaction

The tasks are CommonsenseQA and natural language inference using SNLI. Existing explanations come from CoS-E and ECQA for CommonsenseQA and e-SNLI for SNLI. These datasets differ in annotation quality and instructions. ECQA, for example, asks annotators to explain rejected alternatives as well as the selected answer. The researchers compare explanations within these contexts rather than treating all human-written rationales as equivalent reference material.

The researchers create few-shot prompts from 115 training instances, using between 8 and 24 examples in individual prompts. They compare prompts containing dataset explanations with prompts containing explanations written by the paper's authors. Each task has a fixed 250-instance test set that is separate from prompt design. Human evaluation includes head-to-head preference judgments and absolute ratings along several dimensions, including grammar, factuality, label support, information content, and overall acceptability.

The annotation interfaces are part of the method. Workers see the task instance and its label alongside one or more explanations, then provide the requested comparison or rating. The binary acceptability interface reduces the writing burden, while repeated ratings permit analysis of agreement. The paper reports low-to-moderate agreement in several studies, making subjectivity a measured property of the task rather than an incidental concern.

![The explanation acceptability interface presents the question, its supplied label, and five candidate explanations for human judgment. Source: Wiegreffe et al. (2022), Figure 9, PDF page 26; task panel cropped from the original paper.](figures/wiegreffe2022explanations.png)

#### Overgeneration and filtering

The pipeline generates one greedy explanation and four stochastic alternatives for each instance. The distinction between candidate quality and candidate-set coverage is important. An individual stochastic sample is less likely than the greedy sample to receive unanimous approval, but a set of alternatives is more likely to contain at least one acceptable explanation. For CommonsenseQA, the proportion of instances with a unanimously acceptable explanation rises from 46.3% for the greedy output to 79.5% when the additional samples are considered. For NLI, it rises from 31.5% to 51.2% in that analysis.

A filter must then identify the useful candidate. The researchers collect approximately 6,200 instance-explanation pairs and about 19,000 individual judgments per task, and train T5-Large and T0-3B models to predict acceptability. The filter receives the instance, gold label, and explanation. Baselines include random selection, the generator's negative log likelihood, and explanation-only classifiers that omit the instance context.

The evaluation distinguishes selecting one explanation per instance from classifying explanations independently. The first setting measures how often the selected explanation meets the human acceptability criterion; the second uses average precision. This separation prevents a good candidate-ranking result from being confused with an ability to certify every explanation.

#### Results and limitations

Prompt quality has a substantial effect. With author-written prompts, GPT-3 explanations are preferred to CoS-E explanations in 78.9% of judgments, while the comparison with ECQA and e-SNLI is closer. The result does not show that generated explanations generally surpass human explanations; it shows how the quality of both prompting examples and the human reference dataset affects the comparison.

The learned filter improves selection over likelihood-based ranking. In the reported CommonsenseQA test results, T0-3B obtains 59.9% select-one accuracy under the unanimous-acceptability criterion, compared with 52.0% for the negative-log-likelihood baseline. Context-sensitive models outperform explanation-only baselines, suggesting that the learned judgment includes some relationship between the explanation and the task. Nevertheless, explanation-only models remain competitive enough to indicate that surface features contribute to acceptability predictions.

Filtered explanations improve label support and information content, but gains do not occur on every dimension. Greedy explanations retain advantages in some surface-level attributes. The best filters also remain below the oracle that always selects an acceptable candidate when one exists. Evaluation on a separately recruited set of SNLI annotators provides evidence against complete dependence on the original annotator group, while differences in acceptability remain.

For this review, the paper demonstrates how an interface can organize human judgment into a useful training signal. Its findings concern acceptability and generation quality, not causal faithfulness or improved end-user decision accuracy. This distinction connects it to Jacovi and Goldberg's framework and to later studies of trust: a system can become better at selecting persuasive explanations without establishing that reliance on those explanations is warranted. The appropriate research continuation is to evaluate acceptability alongside correctness, faithfulness, and downstream human performance when those additional claims are made.

### Synthesis of Part I

The foundations establish three separate relationships. Turpin et al. examine the link between input influence and explanation content; Lanham et al. examine the influence of reasoning text on the final answer. Radhakrishnan et al. alter information flow to strengthen some of those relationships. Wiegreffe et al. improve the connection between explanations and human judgments of acceptability. Jacovi and Goldberg explain why these outcomes require different labels and tests.

For the remaining categories, the consequence is practical: identify what the interface exposes before interpreting its evaluation. A display may represent an actual execution dependency, an internal activation, an inferred relationship among sentences, or a human-oriented justification. Each can be useful, but the evidence required to support its claims differs.


## Part II. Model Internals, Representations, and Mechanistic Interpretability

This category follows the synthesis report's broad grouping of work that helps researchers inspect or assess model computation. Its nine papers cover several different objects. BertViz, exBERT, and AttentionViz expose attention and representation structure. LM-Debugger supports interventions in feed-forward updates. The Tuned Lens and Patchscopes decode information from intermediate representations. Semantic uncertainty estimates disagreement among possible meanings, while the two process-supervision papers train verifiers for intermediate solution steps.

The grouping is useful as a research foundation, but its members should not all be called mechanistic interpretability methods. Output uncertainty and process reward models operate at different levels from activation inspection. The reviews identify that level explicitly and distinguish an actual network state from an explanation or score derived from it.

### 6. Vig (2019): BertViz

**Reviewed source:** Vig (2019). *A Multiscale Visualization of Attention in the Transformer Model*.

#### Problem and contribution

Vig (2019) introduces BertViz as a multiscale interface for inspecting transformer attention. A transformer contains many attention heads distributed across layers; examining one attention matrix at a time makes it difficult to locate a relevant pattern or understand how individual attention scores are formed. The paper addresses this problem through coordinated views at the head, model, and neuron levels. It demonstrates the approach on BERT and GPT-2.

The contribution is a visual analysis tool and a set of use cases. It extends earlier attention visualization by adding a model-wide overview and a detailed view of query-key computation. The work does not present a controlled experiment showing that the interface improves analyst performance, nor does it claim that attention alone completely explains a prediction. Its introduction acknowledges limits on attention's value as an explanation of individual decisions.

#### Visual encodings and interaction

The attention-head view duplicates the input tokens in two columns. Curves connect an attending token on the left to attended tokens on the right. Color identifies the attention head, while line weight communicates the attention score. Users select a layer and one or more heads, then filter to a token to reduce visual clutter. For BERT sentence pairs, a sentence-level filter restricts the display to within-sentence or between-sentence attention.

This duplication represents a directed relation. The two occurrences of a token have different roles in the attention computation; they are not two different words in the original input. That distinction is central to reading the image. Token selection makes the relation local enough to inspect, while head selection allows the analyst to compare different learned patterns for the same sentence.

![BertViz shows directed token-to-token attention and lets the analyst select a layer, head, or token. Source: Vig (2019), Figure 1, PDF page 2; cropped from the original paper.](figures/vig2019bertviz.png)

The model view organizes head thumbnails in a matrix whose rows represent layers and whose columns represent heads. This small-multiples arrangement makes coarse patterns visible across the network. The user can select a thumbnail to inspect its tokens in greater detail. The overview therefore supports finding a candidate head before committing to detailed analysis, rather than requiring the user to choose a head by index without visual guidance.

The neuron view exposes the computation behind an attention distribution. It presents the selected query vector, the keys for candidate tokens, elementwise query-key products, dot products, and the resulting softmax weights. A high attention score can then be traced to contributions from vector dimensions. This view changes the question from where attention is directed to how the query-key calculation produces that direction.

#### Demonstrations and findings

The examples identify heads that attend to preceding words, distribute attention broadly, or connect corresponding portions of sentence pairs. Other demonstrations show lexical and syntactic patterns associated with lists, verbs, acronyms, and coreference. These observations illustrate the tool's ability to make hypotheses visible; they do not establish that each head has one exclusive linguistic function.

A gender-bias example compares continuations following prompts that differ in a pronoun. The visualization reveals an attention pattern that associates a feminine pronoun more strongly with a nurse and a masculine pronoun with a doctor in the presented context. The generated continuations and attention display together motivate concern about learned associations. The paper treats the head as a potential source for investigation, rather than demonstrating a general causal account of gender bias across the model.

The model view supports a different task: locating inter-sentence attention relevant to paraphrase analysis. The distinctive crossing pattern in thumbnails helps an analyst identify heads that connect the two inputs. The neuron view then supports inspection of dimensions contributing to an observed pattern. Across these examples, the key result is the practical availability of multiple scales of inspection within one tool.

#### Limitations and role in the collection

BertViz visualizes attention for particular inputs. An appealing pattern in one sentence may not characterize the head across a corpus. The head view can also become crowded as token count or the number of selected heads grows. Filtering and small multiples address navigation, but they do not remove the need for systematic sampling and quantitative validation of a hypothesis.

Attention weights specify how one part of the network combines information; they do not expose all transformations applied to that information or all contributions to the final output. The neuron view provides more detail about the attention calculation, but the display is still a partial account of the model. Jacovi and Goldberg's distinction between interpretability claims and their verification applies directly.

BertViz is the clearest early example in this collection of moving between overview and detail for model inspection. exBERT extends the analysis with corpus-based neighbors and linguistic metadata. AttentionViz changes the overview from many heads for one input to query-key structure across many inputs. LM-Debugger shifts attention from attention weights to feed-forward updates and adds direct intervention. These relationships make BertViz a useful starting point for understanding the visual grammar of the later tools without treating them as interchangeable implementations.

A practical evaluation could ask whether the three views help analysts formulate and test a specific hypothesis about attention. That would measure the interface's analytical value while preserving the paper's distinction between a visible pattern and its explanation.

### 7. Hoover et al. (2020): exBERT

**Reviewed source:** Hoover et al. (2020). *exBERT: A Visual Analysis Tool to Explore Learned Representations in Transformer Models*.

#### Problem and contribution

Hoover et al. (2020) develop exBERT to connect attention patterns with information represented in contextual embeddings. An attention line can show that one token attends to another, but it does not by itself explain what information the attended representation contains. exBERT combines an interactive attention display with nearest-neighbor search over an annotated corpus. The analyst can move from a local observation to examples of similar representations and summaries of their linguistic properties.

The paper's contribution is a hypothesis-generation environment. Its evaluations demonstrate that users can reproduce findings from prior analyses and extend observations to another model. The authors explicitly position local interactive exploration as a precursor to larger statistical tests. This framing is more precise than treating corpus search results as a definitive interpretation of a head's global function.

#### Interface and data preparation

The attention view shows duplicated token columns connected by directed attention curves. Users select layers and heads, hover over tokens to filter incoming or outgoing attention, and click to retain a selection. The interface also displays the model's top predictions. In bidirectional models, users can mask a token and inspect the predicted replacement; in autoregressive models, predictions refer to the following token.

Two matrices summarize attention entering and leaving tokens across heads. A control can hide special tokens and renormalize the remaining attention. This supports investigation of patterns otherwise obscured by tokens receiving large amounts of attention, but it also changes the displayed distribution. An analyst should distinguish a filtered, renormalized view from the unmodified weights when interpreting apparent strength.

![The exBERT overview links attention inspection to nearest-neighbor contexts and linguistic summary histograms. Source: Hoover et al. (2020), Figure 1, PDF page 2; cropped from the original paper.](figures/hoover2020exbert.png)

The corpus view searches for representations similar to the current selection. Before use, the corpus is split into sentences, annotated with metadata such as part of speech and dependency labels, processed by the model, and indexed for cosine-similarity search. The paper uses a FAISS index and displays the 50 most similar tokens with their surrounding contexts. Histograms summarize metadata for the matched token and the token receiving its strongest attention.

The tool supports both layer embeddings and a context representation derived from normalized attention-head outputs before the final projection within the attention block. Restricting the selected heads changes the representation used for search. This allows an analyst to ask whether a particular head or head combination carries a recognizable linguistic pattern, rather than searching only the aggregate representation after all heads have been combined.

#### Case studies

The BERT case study examines heads associated with auxiliary verbs, preposition-object relationships, and possible coreference. For a masked verb, the analyst can inspect attention to an auxiliary and then examine whether nearby corpus representations also correspond to verbs in similar contexts. The combination of individual examples and aggregate metadata provides a stronger basis for a hypothesis than a single attention diagram alone.

The paper also follows a masked token through layers. In the illustrated example, the nearest neighbors of an early masked representation do not provide a clear verb signal, while later representations increasingly do. Information in selected head outputs can appear earlier than in the aggregate embedding. This demonstrates why the tool exposes more than one representation type and why conclusions depend on exactly which state is inspected.

The GPT-2 case study compares pronoun predictions in sentences containing nurse and doctor. In the reported example, the model assigns 90% probability to a feminine pronoun after the nurse context and 6% to the masculine alternative; substituting doctor produces a different distribution. The attention patterns in the final layers appear similar despite the change in prediction. This is a useful example of the limits of interpreting attention geometry alone.

Other GPT-2 examples examine auxiliary and direct-object patterns. Because an autoregressive model cannot attend to future tokens, the analyst must interpret attention and corpus metadata relative to the next-token prediction task. exBERT adapts the corpus summaries accordingly. The same visual component therefore has model-dependent semantics, an issue that should be explicit in comparisons across architectures.

#### Evidence limits and relationship to other tools

The paper does not establish a measured improvement in debugging accuracy or speed through a controlled user study. Its evidence consists of case studies that reproduce or extend known observations and demonstrate a feasible analysis workflow. The authors note that a small set of neighbors for one token cannot establish a head's global behavior. Corpus composition, annotation accuracy, and the similarity metric all affect what the user sees.

Nearest-neighbor retrieval also describes representational similarity, not necessarily causal importance. A model may encode a property without relying on it for the prediction under examination. Users need interventions or additional behavioral tests to connect a retrieved pattern to an outcome. These limits do not negate the tool's contribution; they identify its role in a broader research process.

Within the collection, exBERT connects BertViz's local attention inspection to broader evidence across input contexts. AttentionViz later offers a different global strategy by projecting query and key vectors from many inputs into a shared space. The Tuned Lens provides vocabulary predictions rather than corpus neighbors, while Patchscopes decodes selected information through a new model computation. Comparing these tools by the question each representation can answer is more informative than comparing them only by screen layout.

### 8. Yeh et al. (2024): AttentionViz

**Reviewed source:** Yeh et al. (2024). *AttentionViz: A Global View of Transformer Attention*.

#### Problem and contribution

Yeh et al. (2024) address the difficulty of identifying attention patterns across many input sequences. Earlier displays often show one sentence or image at a time, leaving analysts to remember and compare separate views. AttentionViz jointly projects query and key vectors from multiple inputs, producing a visual signature for each attention head. The system connects those signatures to detailed views of individual sentences and image patches.

The main contribution is the query-key representation and its coordinated exploration. The tool supports language and vision transformers, including BERT, GPT-2, and ViT configurations. It uses t-SNE, UMAP, and PCA rather than relying exclusively on t-SNE, as a brief description might imply. Each projection offers a different view of the underlying high-dimensional data, and the interface lets analysts compare them.

#### Representation and interaction

Attention depends on query-key dot products followed by normalization. A scatterplot, however, communicates distance. The authors therefore examine how to make distance in a joint representation informative about attention. They translate key vectors to align centroids and apply reciprocal scaling to queries and keys. These transformations preserve the relevant attention computation while improving the relationship between geometric proximity and query-key compatibility before dimensionality reduction.

The distinction between this mathematical normalization and the subsequent projection is important. Preserving attention under a high-dimensional transformation does not guarantee that every two-dimensional distance faithfully represents attention. The authors evaluate the relationship empirically and retain detailed attention displays to check interpretations drawn from the projection. The image should therefore be read as an exploratory summary rather than a literal map of all information flow.

![AttentionViz connects a matrix of attention-head projections to a selected head and a sentence-level attention view. Source: Yeh et al. (2024), Figure 5, PDF page 5; cropped from the original paper.](figures/yeh2023attentionviz.png)

The matrix view shows one projection per head, arranged by layer and head index. Analysts can scan for distinctive shapes, switch datasets or projection methods, and search across the matrix. The single-head view supports zooming, token search, and alternative color encodings. Selecting a point highlights other tokens from the same input, connecting an aggregate pattern back to its source context.

The sentence view uses directed token relationships; the image view shows the selected patch in its original image, an attention heatmap, and alternative arrow displays. The system can show only the strongest relationship or a thresholded set of relationships to control clutter. Color can identify query versus key, token position, vector norm, or image row and column. For image data, displaying the patches themselves provides an additional interpretable encoding.

#### Evaluation and findings

The design process includes initial interviews with five machine-learning researchers. A later feedback round involves four experts, including returning participants and new experts. The paper combines their observations with application scenarios. This provides evidence of research utility and interpretable discoveries, but it is not a controlled comparison of task performance against another visualization tool.

The vision examples use synthetic gradients and spatial patterns to investigate attention specialization. The authors identify heads whose structure corresponds to hue, brightness, spatial frequency, or orientation. They then inspect attention in the original image to check whether the apparent grouping corresponds to relationships among patches. Other examples show a progression from local spatial relationships in early layers to broader row- or column-related attention.

In BERT, distinctive projection shapes help locate positional and semantic patterns. Spiral-like or clustered layouts can correspond to offsets between token positions; the sentence view provides a check on that interpretation. Dataset-specific patterns also appear in later heads when the task involves comparing sentences. Search results across the matrix offer another way to distinguish patterns dominated by position from those involving related token meanings.

The GPT-2 analysis identifies differences between query and key norms and widespread attention to the first token. These observations generate questions for further research rather than resolving their causes. The authors also report preprocessing and memory constraints: the demonstrated system uses precomputed projections and bounded samples, with larger inputs increasing latency. The word global therefore means an overview across the sampled inputs and heads, not exhaustive coverage of every possible model input.

#### Limitations and comparative value

Projection distortion, sampling, and the choice of color encoding influence what patterns become visible. A visually distinctive cluster can motivate an explanation that still needs quantitative or causal testing. The tool focuses on attention weights and query-key relationships; it does not show the complete content transmitted through value vectors or establish the contribution of every head to final task performance.

AttentionViz extends the overview-and-detail pattern of BertViz to a different aggregation level. exBERT searches for similar contexts around a selected representation; AttentionViz exposes a broader geometry that helps analysts decide what to select. Its coordinated views also anticipate a recurring pattern in the later reasoning-interface papers: an overview reduces navigation cost, while a linked source view supports verification. The transferable design principle is the connection between abstraction and inspectable evidence, with the limits of the abstraction made explicit.

For a follow-up study, analysts could record hypotheses before and after using the global view, then test those hypotheses against held-out inputs. Such an evaluation would distinguish useful pattern discovery from a persuasive account of the displayed sample.

### 9. Geva et al. (2022): LM-Debugger

**Reviewed source:** Geva et al. (2022). *LM-Debugger: An Interactive Tool for Inspection and Intervention in Transformer-Based Language Models*.

#### Problem and contribution

Geva et al. (2022) introduce a debugger that exposes changes to token representations produced by transformer feed-forward layers and lets users intervene in those changes. The tool treats the evolving hidden representation as a distribution over vocabulary items and decomposes a feed-forward update into weighted contributions from value vectors. Users can inspect which tokens those vectors promote and alter their contribution during generation.

This contribution differs from displaying a model-generated explanation. LM-Debugger accesses internal model components and changes activation coefficients. It also differs from an attention viewer because its primary object is the feed-forward update. The paper combines per-input tracing with input-independent search over value vectors, giving users two ways to identify an intervention candidate.

#### Representation and interface

The underlying method projects the token representation before and after a feed-forward update into the output vocabulary. It also projects individual value vectors to identify tokens they tend to promote. A value vector is a static model parameter; its weighted contribution to an update depends on the current input. Keeping these two objects separate is necessary to understand what a search result and a prediction trace represent.

The prediction view shows top vocabulary items across layers and the ten most dominant feed-forward sub-updates for each layer. Each sub-update has a layer-and-dimension identifier and an input-dependent coefficient. Selecting it reveals the associated vocabulary projection. Users can name value vectors, which helps maintain a working interpretation across successive experiments.

![LM-Debugger's prediction view links layer-by-layer vocabulary changes to an intervention panel and value-vector details. Source: Geva et al. (2022), Figure 2, PDF page 3; cropped from the original paper.](figures/geva2022lmdebugger.png)

The intervention panel allows a user to turn a selected vector off by setting its coefficient to zero, or turn it on using the coefficient of the dominant sub-update in that layer. Configured interventions remain active during generation. This is a specific activation manipulation, not unrestricted editing of the model's learned weights or a guaranteed semantic command. The user observes the changed output to determine whether the selected intervention had the desired effect.

The exploration view searches the top vocabulary tokens associated with value vectors using a text index. It also groups vectors by similarity and displays token summaries for a cluster. An analyst interested in a concept can search for related words, inspect candidate vectors, and expand from a seed vector to nearby vectors. The resulting set can then be used in the prediction view.

#### Demonstrations

One case study traces an ambiguous continuation such as a book being for a purpose or for a person. The displayed vocabulary distribution shifts across layers from terms associated with purpose toward terms associated with an audience. Inspection of dominant sub-updates helps connect that shift to particular value vectors. The example illustrates a way to investigate prediction construction without requiring the model to describe the process in prose.

A second demonstration changes occupation-related predictions after a prompt about a wife working as something. Searching for software-related concepts identifies two value vectors. Activating them shifts prominent predicted tokens toward software and programming occupations. The paper reports that this intervention involves only 0.002% of the network's relevant vectors. That fraction describes the size of the intervention in the demonstrated model; it does not establish a general formula for correcting occupational bias.

The sentiment example selects a small group of vectors associated with positive or negative language and applies them to continuations of Yelp-derived inputs. The paper presents short generated continuations under each condition. These examples show that selected internal updates can influence generation in interpretable directions. They do not constitute a broad benchmark of sentiment control, output quality, or preservation of unrelated capabilities.

The implementation uses separate prediction and exploration applications, with model execution, a search index, and precomputed vector clusters behind the interface. The released implementation focuses on GPT-2 models. The authors describe adaptation to other autoregressive models as possible with local changes; compatibility should not be assumed for arbitrary architectures without implementing and checking those changes.

#### Limitations and place in the review

Vocabulary projection is an interpretive device. A list of promoted tokens can suggest a concept, but the vector's contribution may be context-dependent and more complex than a short human label. Interventions can also alter fluency or unrelated behavior. The demonstrations show feasibility and selected effects, while a deployment-quality steering claim would require broader measurements of reliability and side effects.

The paper's evidence is principally technical demonstration and case analysis rather than a controlled user study. A changed output establishes that an intervention had an effect, but the completeness of the explanation still depends on how well the selected vector and the rest of the model computation are understood. The interface does not eliminate the need for causal controls or systematic evaluation.

LM-Debugger is a useful bridge between the inspection tools and the steering tools in later categories. Its manipulation acts on activation coefficients, while Hippo and other reasoning interfaces act on generated text or structured reasoning nodes. These operations should be compared by what they change in the computation, not merely by whether both offer an edit control. The Tuned Lens addresses limitations in direct vocabulary projection, and Patchscopes generalizes the use of activation interventions to decode and redirect information.

### 10. Belrose et al. (2023): The Tuned Lens

**Reviewed source:** Belrose et al. (2023). *Eliciting Latent Predictions from Transformers with the Tuned Lens*.

#### Problem and contribution

Belrose et al. (2023) develop the Tuned Lens to decode intermediate transformer states into vocabulary distributions more reliably than direct application of the final unembedding matrix. The earlier logit-lens approach can produce useful intermediate predictions for some models but fails or becomes biased for others. Representations change across layers, so an operation designed for the final layer may misread an earlier state.

The Tuned Lens learns an affine translator for each layer while leaving the underlying language model frozen. The translator maps an intermediate representation into a form that can be decoded with the model's final output transformation. The resulting sequence of vocabulary distributions is called a prediction trajectory. The paper evaluates predictive quality, causal relationships, and several applications of these trajectories.

#### Method and visual representation

Training uses the model's final distribution as the target, minimizing a distillation loss rather than learning from external class labels. This choice aims to recover the model's predictions without encouraging the probe to learn a separate task solution from ground-truth supervision. The learned component is a hidden-dimension transformation rather than a new full vocabulary classifier for every layer, reducing the parameter and training burden relative to that alternative.

The visual representation places input positions along one axis and layers along the other. A cell shows a high-probability vocabulary prediction, with color communicating probability. The reader can inspect when a prediction becomes recognizable, when it changes, and how it approaches the final output. This is a visualization of decoded hidden states across depth, not a chronological transcript of sentences generated during autoregressive reasoning.

![The Tuned Lens comparison shows vocabulary predictions across layers and token positions, exposing interpretable intermediate predictions where the direct logit lens is less informative. Source: Belrose et al. (2023), Figure 1, PDF page 1 of version 6; cropped from the original paper.](figures/belrose2023tunedlens.png)

The method addresses both average bias and representational drift. An offset can compensate for missing average residual contributions, while a matrix can adjust the basis in which features are represented. The paper examines covariance changes across layers and shows that translators often transfer to nearby layers with modest penalties. It also studies transfer from a base model to a fine-tuned derivative, supporting reuse in some settings without implying universal compatibility.

#### Evaluation and findings

The experiments cover several autoregressive model families, including Pythia and models up to GPT-NeoX-20B. The Tuned Lens produces lower-perplexity intermediate predictions and less systematic vocabulary bias than the logit lens in the reported evaluations. The improvement is especially useful where direct projection produces implausible repeated tokens or appears to reconstruct the input instead of predicting a continuation.

The paper goes beyond predictive agreement by examining causal fidelity. Causal basis extraction identifies directions that strongly affect the lens output, then tests their influence on the original model. In the illustrated Pythia-410M layer, the reported Spearman correlation between influence on the lens and influence on the model is 0.89. A second analysis examines whether interventions move the two distributions in aligned directions. These experiments provide evidence that the lens uses some features relevant to the model rather than only a correlational shortcut.

Applications include studying the effect of misleading few-shot demonstrations and detecting a particular family of prompt-injection inputs through prediction trajectories. The detection experiments attain near-perfect AUROC on several tasks, but performance varies and a representation-based baseline is competitive or better in some cases. The result should therefore be described as an experimental use of trajectory features, not a general solution to prompt-injection detection.

The locally saved revision contains an important update: the authors report that Muon substantially improves lens training compared with their original SGD procedure and state that earlier lenses were undertrained. They do not rerun all earlier experiments with the new optimizer. The revision also reports mixed results for eliciting hidden taboo-word information, with the Tuned Lens outperforming the logit lens at some layers and underperforming at others. A review of this local version must include those qualifications rather than summarizing only the original release.

#### Limitations and comparative role

A learned decoder is still an approximation. Agreement with the final distribution does not establish a complete account of every intermediate computation, and causal tests on selected directions do not exhaust all relevant features. Layer choice, training quality, and the target model affect interpretation. The revised manuscript's optimizer discussion makes the measurement-tool dependence particularly concrete.

The paper belongs with model inspection rather than user-facing CoT editing. Its rows represent network depth; ReTrace's timeline and Hippo's tree represent generated reasoning activities or user-visible structure. Confusing those objects would imply a direct correspondence that the papers do not establish. The visualization is useful precisely because it gives access to a different level of evidence.

The Tuned Lens complements LM-Debugger by improving a vocabulary-decoding operation used in many inspection workflows. Patchscopes places such methods in a broader framework and uses continued model computation to extract information. Together, these papers support a research agenda in which visual interfaces disclose the decoder and transformation used to produce a displayed interpretation, so readers can distinguish a raw model state from an inferred vocabulary-level account.

An interface built around this method should retain the lens-training configuration with each saved view. Otherwise, a change in the displayed trajectory could reflect a changed measurement procedure rather than a changed behavior of the underlying model.

### 11. Ghandeharioun et al. (2024): Patchscopes

**Reviewed source:** Ghandeharioun et al. (2024). *Patchscopes: A Unifying Framework for Inspecting Hidden Representations of Language Models*.

#### Problem and contribution

Ghandeharioun et al. (2024) propose Patchscopes as a configurable framework for decoding information from hidden representations. The core operation takes an activation from a source computation and inserts it into a target computation designed to express a particular kind of information. The target model then continues generating. Different choices of prompt, layer, token position, model, and transformation produce different inspection methods.

The contribution has two parts: a framework that expresses several existing methods as configurations of one operation, and new configurations for token prediction, attribute extraction, entity resolution, and reasoning-error correction. It provides a useful conceptual bridge between vocabulary projection and activation patching. It is principally a technical inspection framework, not a controlled evaluation of an end-user interface.

#### Data flow and interpretation

The source prompt is processed to a selected hidden state. An optional transformation maps that state into the target model's representation space. The target prompt is processed to a selected layer and position, where its state is replaced by the transformed source state. Continuing the target computation produces the observable output. In a token-identity configuration, examples of copying strings encourage the model to decode the inserted representation as a token or entity identity.

![Patchscopes transfers a selected hidden representation from a source execution into a target prompt designed to decode it. Source: Ghandeharioun et al. (2024), Figure 1, PDF page 1; cropped from the original paper.](figures/ghandeharioun2024patchscopes.png)

The interpretation has a boundary that the paper states explicitly. The target model can add information during continued computation. A generated description therefore shows what can be decoded from the patched representation with that target computation; it does not guarantee that every word of the description was already stored in the original vector. Removing the source context prevents additional source-context information from entering after patching, but it does not remove the target model's knowledge.

This boundary matters when comparing Patchscopes with probing or a direct vocabulary projection. A richer explanation may be more informative to a reader while also depending on a more powerful decoding process. The framework makes these choices explicit. Some configurations require learned mappings, especially across models; others operate without task-specific training.

#### Experiments and findings

The token-prediction experiments compare a token-identity Patchscope with vocabulary-projection baselines across several language models. The reported configuration performs better in many intermediate and later layers, while the earliest layers remain difficult. The paper's Tuned Lens baseline uses an affine representation-mapping procedure, so its numerical comparison should be interpreted according to that implementation rather than assumed to represent every possible training procedure for the Tuned Lens.

For attribute extraction, the researchers filter a collection of factual and commonsense relations to 12 tasks with sufficient examples, yielding 1,453 data points. Target prompts ask for a property of a subject whose representation is patched into the prompt. Patchscopes significantly outperform logistic-regression probes on six tasks and perform comparably on most others. The evaluation counts an extraction as successful if a suitable target layer produces the expected object within the generated continuation. That search-based success criterion is more permissive than fixing one layer in advance for deployment.

Entity-resolution experiments use popular and rare entities from PopQA. The generated descriptions show how representations can shift from a final name fragment toward a complete entity across early layers. The authors compare descriptions with reference descriptions and inspect qualitative examples. Cross-model experiments show that a larger model in the same family can sometimes decode a smaller model's representation more effectively, although the benefit is not universal across model families and conditions.

The multi-hop experiment selects cases in which the model can answer the component relations independently but struggles with their composition. From 1,104 generated queries, 46 satisfy the stated selection criteria. The Patchscope achieves 50% accuracy, compared with the paper's reported 35.71% CoT baseline and 19.57% vanilla baseline. The researchers use known query structure and search source-target layer combinations; they explicitly frame this as a proof of concept rather than a directly comparable general-purpose replacement for CoT.

#### Limitations and relationship to the collection

Patch placement and target-prompt design materially affect the output. Placeholder information can contaminate later generation, and cross-model use depends on compatible mappings. A decoded statement may combine information from the source representation with the target model's prior knowledge. These limitations require careful attribution when a visualization presents the generated text as an interpretation of an internal state.

The framework also highlights a difference between locating information and proving that the original model used it. Decodability can reveal an available capability or representation without establishing its causal role in the unmodified prediction. Interventions provide additional evidence, but the interpretation must remain tied to the exact experiment performed.

Within the collection, Patchscopes offers a way to connect internal-state inspection with interventions that alter reasoning outcomes. It complements Radhakrishnan et al.'s context isolation at the prompt level and LM-Debugger's manipulation of feed-forward contributions. It also provides a caution for later natural-language trace tools: explanatory text can be generated by an additional interpretation process. Interfaces should preserve the distinction between observed source material, transformation, and inferred explanation, especially when a user is asked to trust or revise the resulting representation.


### 12. Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation

**Reviewed source:** Kuhn et al. (2023). *Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation*.

#### Problem and contribution

Kuhn, Gal, and Farquhar (2023) examine uncertainty when a language model can express the same answer in many ways. Token probabilities distribute mass across particular strings. A model may therefore appear uncertain because it produces several paraphrases, even when those paraphrases make the same claim. Conversely, fluent repetition of one false claim can appear highly confident. The paper addresses the first problem by defining uncertainty over meanings rather than treating every surface form as a different answer.

Semantic entropy groups sampled responses into semantic equivalence classes and estimates entropy over those classes. The contribution is a practical approximation to meaning-level uncertainty, evaluated as a way to distinguish correct from incorrect answers. It does not introduce a user interface, and it does not test whether generated explanations faithfully describe internal computation. Its place in this collection is as a possible signal that an interface could use to prioritize inspection.

#### Method and assumptions

The method samples multiple answers to the same question. A natural-language inference model checks whether two answers entail each other when each is considered with the question. Bidirectional entailment is the operational criterion for semantic equivalence. The procedure groups equivalent responses, combines their estimated probability mass, and calculates entropy across the resulting groups. Several formulations account for the dependence of sequence likelihood on answer length.

Conditioning equivalence on the question matters. A short response that is ambiguous in isolation can be a complete answer in context. Requiring entailment in both directions also prevents a more specific answer from being equated automatically with a broader statement. However, the clustering remains an approximation made by another learned model. Errors in entailment judgments change the apparent number and probability of meanings.

The experiments use OPT language models from 2.7 billion to 30 billion parameters as generators and a pretrained DeBERTa inference model for clustering. The approach avoids retraining the generator or collecting task-specific correctness labels to fit the uncertainty measure. References to using a single model should be read as using a single answer-generating model, rather than an ensemble of generators. The procedure still relies on an auxiliary inference model, with its own training history and limitations.

#### Evaluation and findings

The main evaluation uses open-book CoQA and closed-book TriviaQA question answering. The authors compare semantic entropy with measures that operate on strings, predictive probabilities, and related uncertainty baselines. Correctness is assessed with an automatic answer-matching procedure, including a ROUGE-L threshold in the principal experiments; appendices examine alternative scoring choices. This makes the evaluation practical, but the outcome is partly dependent on the chosen definition of an acceptable answer.

Semantic entropy achieves reported AUROC values of approximately 0.77 on CoQA and 0.83 on TriviaQA in the comparison with a simple count of semantic clusters. Counting clusters alone produces approximately 0.66 and 0.79. Incorporating their probability mass therefore adds information beyond measuring response diversity. These are discrimination results: the measure helps rank cases by their likelihood of being wrong. They should not be restated as proof that a displayed percentage is a calibrated probability of correctness.

The authors also inspect the semantic-equivalence procedure using human judgments on 300 generations. Reported agreement with the desired equivalence decisions is 95.5% for CoQA and 92.7% for TriviaQA. This supports the practical use of entailment clustering in these settings while leaving a measurable source of uncertainty within the uncertainty estimator itself.

The analysis of ten samples per question illustrates the intended mechanism. Correct answers produce fewer distinct meanings on average than incorrect answers: 1.27 versus 1.77 clusters on CoQA and 1.89 versus 3.89 on TriviaQA. Sampling temperature and sample count affect the result. Too little diversity provides little evidence of competing meanings, while very high temperature can produce low-quality answers that distort the estimate. A temperature of 0.5 works well in the tested settings, but this is an experimental choice rather than a universal constant.

#### Limitations and relationship to the collection

Semantic consistency does not establish truth. If the generator repeatedly gives the same wrong answer, its semantic entropy can be low. The measure cannot, by itself, detect a confidently repeated misconception or an explanation that consistently omits a causal influence. This is precisely where the distinction established by Turpin et al. and Jacovi and Goldberg remains necessary: agreement across outputs concerns their content, not their faithfulness to the process that produced them.

The implementation also incurs repeated generation and entailment costs. Meaning equivalence becomes harder for long responses containing several claims, partial agreement, qualifications, or contradictions. An interface that collapses such responses into one confidence indicator could hide the location of disagreement. The paper's question-answering experiments do not establish performance for arbitrary multi-step agent traces or open-ended collaborative writing.

For later systems in this collection, the useful design implication is to expose uncertainty with its provenance. A display could show alternative answer clusters, the sampled responses supporting each cluster, and the limits of the estimator. This would let a user inspect disagreement rather than merely accept a score. Pairing semantic uncertainty with step verification could also distinguish disagreement about the final answer from a suspected local error, although that combination requires its own evaluation. The paper supplies a technically grounded signal for such work, not evidence that displaying it necessarily improves human judgment.

### 13. Let's Verify Step by Step

**Reviewed source:** Lightman et al. (2024). *Let's Verify Step by Step*.

#### Problem and contribution

Lightman et al. (2024) compare supervision of intermediate mathematical steps with supervision of final outcomes. An outcome reward model can reward a solution that arrives at the right answer through an invalid argument. A process reward model receives labels on the individual steps, allowing it to identify an earlier failure even when the final answer happens to be correct. The research question concerns the effectiveness and cost of these supervision strategies for selecting mathematical solutions.

The paper contributes process-supervised reward models, the PRM800K dataset, an annotation workflow, and experiments comparing process and outcome supervision. Its primary evaluation uses reward models to choose among generated solutions. The generators are held fixed in those comparisons. The paper should therefore not be summarized as demonstrating reinforcement learning of the generator with process rewards; that is a separate contribution of Math-Shepherd in the next review.

#### Annotation and verification workflow

Human labelers inspect a solution step by step and mark a step positive, negative, or neutral. Positive steps are correct and reasonable; negative steps are incorrect or unreasonable; neutral labels accommodate ambiguity. Annotation focuses on the first error rather than requiring reliable labels for every continuation after a solution has already gone wrong. PRM800K contains approximately 800,000 step labels from 75,000 solutions to 12,000 problems.

![The PRM800K annotation interface presents mathematical reasoning one step at a time for human correctness judgments. Source: Lightman et al. (2024), Figure 1, PDF page 3; cropped from the original paper.](figures/lightman2024verify.png)

The process reward model predicts the label distribution for each step. The main selection rule combines the predicted probabilities that the steps are correct, using their product to score a complete solution. An outcome reward model instead assigns a solution-level score. Both can support best-of-N selection: generate N candidates and return the one with the highest score. This is a search procedure with a potentially large inference budget, not the accuracy of one unaided completion.

The human interface is an important component of the contribution because the supervision depends on consistent local judgments. Its labels are also narrower than a universal assessment of reasoning quality. Mathematical validity, reasonableness, ambiguity, and the position of the first error all shape what the reward model learns. A colored trace produced by that model is a prediction about those judgments; it is not a direct view of the generator's hidden computation.

#### Experimental evidence

The large-scale experiments use a GPT-4-family base model with additional mathematical training. The authors reserve 500 MATH test problems for evaluation and use the remaining 4,500 test problems in the training-data collection process. On that held-out subset, the process reward model selects correct solutions for 78.2% of problems when choosing from 1,860 candidates. The reported outcome reward model reaches 72.4%, and majority voting reaches 69.6% under the corresponding comparison. The subset and candidate budget are essential to interpreting these figures.

The large process and outcome training sets differ in collection strategy and size. Process examples are selected with active learning, while outcome examples include many uniformly sampled solutions. The authors therefore add smaller, more controlled experiments that use a large process model as an automated supervisor. Those experiments allow closer comparisons between process supervision, outcome supervision, and final-answer checking with matched generation settings.

Process supervision performs better in these controlled experiments. The active-learning analysis further estimates an approximately 2.6-fold improvement in data efficiency in its surrogate setting. The selection procedure emphasizes convincing but incorrect solutions while retaining some other examples. This result supports targeted annotation as a practical way to spend labeling effort. It does not imply that every iterative active-learning configuration succeeds; the paper also reports instability in an attempted iterative procedure.

Additional tests use problems from examinations outside the main MATH evaluation. The process model performs better than the outcome model and majority voting in the reported aggregate comparison. These results offer evidence of some transfer within mathematical and scientific problem solving. They do not establish generalization to arbitrary domains, where step boundaries, ground truth, and acceptable justification can be much less clear.

#### Limits and connection to human verification

The paper acknowledges possible pretraining contamination and differences between the largest training conditions. Relative comparisons under shared conditions are more informative than treating the headline score as a general measure of mathematical competence. GSM8K appears in the discussion of related work; it is not a second principal benchmark supporting the main headline result in this paper.

Process supervision also depends on the reliability and coverage of local labels. A reward model may miss a subtle error, over-penalize an unconventional valid step, or assign scores that do not transfer to a different generator. Combining step probabilities compounds uncertainty and favors some solution structures over others. The successful selection experiments do not show that every step score is calibrated or that users understand its meaning.

Within the collection, this work connects formal model evaluation to interface design through the annotation unit. It shows that intermediate steps can carry useful supervision beyond final answers. Later verification interfaces can build on that idea by making steps inspectable, but they must separately test whether users detect errors, identify dependencies, and respond appropriately to model scores. The strongest supported conclusion is that process labels improved solution selection in the studied mathematics settings. Whether the same signals improve human oversight remains an HCI research question.

### 14. Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations

**Reviewed source:** Wang et al. (2024). *Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations*.

#### Problem and contribution

Wang et al. (2024) address the cost of collecting process labels for mathematical reasoning. Math-Shepherd generates approximate step labels automatically by asking whether a solution prefix can be completed to the known correct answer. A process reward model learns from these labels and is then used both to select generated solutions and to provide intermediate rewards during reinforcement learning. This extends the process-supervision theme beyond the fixed-generator selection experiments in Lightman et al.

The central approximation is consequential: a step is treated as promising when a continuation model can reach the correct answer from it. This estimates the usefulness of a prefix for successful completion under that model and sampling procedure. It does not directly prove that the step is logically valid. A capable completer may repair an earlier mistake, and a weak completer may fail after a valid but difficult step.

#### Automatic labeling and system operation

For each intermediate step, the system samples several continuations and checks their final answers. Hard estimation assigns a positive label if at least one continuation reaches the correct answer. Soft estimation uses the fraction of successful continuations. These alternatives encode different assumptions about whether occasional successful recovery or typical successful continuation should determine a prefix's quality.

The default data-construction setup uses a seven-billion-parameter Llemma completer with eight continuations. The resulting training material contains roughly 170,000 GSM8K solutions and 270,000 MATH solutions. The learned process model scores individual steps. For solution verification, the paper primarily uses the minimum step score as the complete solution's score, emphasizing its weakest step. This differs from the product aggregation in Let's Verify Step by Step and is relevant when comparing results across the two papers.

![Math-Shepherd constructs step labels through sampled continuations and uses the resulting process verifier for selection and reinforcement learning. Source: Wang et al. (2024), Figure 1, PDF page 4; cropped from the original paper.](figures/wang2024mathshepherd.png)

The system can select the highest-scoring candidate or combine verifier scores with answer agreement through weighted self-consistency. During reinforcement learning, it delivers process rewards at step endings rather than only at the end of the entire response. The paper evaluates these uses separately, which prevents a gain from extensive candidate search from being mistaken for an improvement in the generator's single-response accuracy.

#### Evaluation and findings

Verification experiments sample 256 candidates per question and report results across three sampling groups. They evaluate the full GSM8K test set and a 500-problem MATH subset. The reinforcement-learning experiments use the full MATH test set. These differences in evaluation population matter when figures from separate tables are compared.

For a Mistral seven-billion-parameter generator initialized from MetaMath training, process-reward reinforcement learning raises greedy accuracy from 77.9% to 84.1% on GSM8K and from 28.6% to 33.0% on MATH. The corresponding outcome-reward model reaches 81.8% and 31.3%. A Llama seven-billion-parameter configuration also improves, from 66.6% to 73.2% on GSM8K and from 19.2% to 21.6% on MATH. These results support a benefit from intermediate rewards in the tested training conditions.

Combining the process-trained Mistral generator with verifier-weighted self-consistency reaches 89.1% on GSM8K and 43.5% on the MATH subset. Those scores include candidate generation and selection; they are not greedy results. With DeepSeek-67B, the paper reports 93.3% GSM8K accuracy using process verification and 48.1% on the MATH subset with the weighted combination. The best configuration differs by benchmark, so these numbers should not be represented as one uniform operating condition.

An examination-based case study also compares selection strategies on 33 Hungarian mathematics questions. The reported score rises from 46 for greedy generation to 54 with outcome verification and 63 with process verification under the paper's candidate-search setup. This is useful supporting evidence on a small additional test, not a broad estimate of transfer across education systems or mathematical disciplines.

#### Label quality and limitations

The authors compare automatic labels with human judgments on 160 GSM8K steps. A stronger completer improves label quality; one reported hard-estimation configuration with a 70-billion-parameter completer and four continuations reaches 86% agreement. Increasing the number of attempts can also increase false positives under hard estimation because one lucky recovery is enough to label a prefix positively. More computation does not necessarily make the proxy monotonically more faithful to human judgments of step validity.

Comparisons with PRM800K are affected by differences in the solution-generating models, data distributions, and training-set sizes. The automatically collected data are substantially larger in the relevant comparison. The results therefore do not establish that automatic labels are intrinsically superior to human process annotations. They show that a particular scalable labeling strategy can train useful verifiers under the tested conditions.

Math-Shepherd introduces no dedicated end-user verification interface. Its original method figure is included because the distinction among continuation sampling, label construction, verification, and reinforcement learning is central to understanding the contribution. If these scores are later displayed in an interface, that distinction should remain visible. A green step could mean that sampled continuations often succeed, not that a human or formal proof checker has certified the step.

The paper supplies an economical bridge from known final answers to intermediate supervision. It complements semantic uncertainty, which measures disagreement among meanings, and Lightman et al., which learns from human step judgments. Each signal has a different evidential basis. Combining them may improve an oversight system, but the collection does not justify treating any one of them as a complete account of correctness, causal faithfulness, or human comprehensibility.

### Part II synthesis: distinguish the evidence behind the display

Part II contains several kinds of access to model behavior. BertViz, exBERT, and AttentionViz support exploration of attention and representations. LM-Debugger and Patchscopes permit interventions, while the Tuned Lens learns a translation from intermediate states to output predictions. Semantic entropy estimates disagreement among generated meanings. The two process-supervision papers learn scores for mathematical steps from different sources of labels.

These methods cannot be placed on one simple scale of explanation quality. Their observations, interventions, and evaluation targets differ. A useful interface must communicate whether a displayed element is an attention weight, a decoded representation, a causal intervention result, a sampled disagreement, a human-derived judgment, or an automatically estimated continuation score. That provenance becomes especially important in the visual workflow systems reviewed next, where several such signals could appear in the same workspace.


## Part III: User Interfaces, Visual Programming, and Development Toolkits

The third part follows the synthesis report's grouping of seven systems for working with LLM applications and outputs. Their common concern is the organization of work around model calls. AI Chains and PromptChainer expose task decomposition; ChainForge and LLM Comparator support comparison and evaluation; AgDebugger and WaitGPT expose execution for debugging; CoAuthor records interaction during collaborative writing. These systems make different units visible, ranging from a prompt node to a code operation or an accepted writing suggestion.

### 15. AI Chains: Transparent and Controllable Human-AI Interaction by Chaining Large Language Model Prompts

**Reviewed source:** Wu, Terry, and Cai (2022). *AI Chains: Transparent and Controllable Human-AI Interaction by Chaining Large Language Model Prompts*.

#### Problem and contribution

Wu, Terry, and Cai (2022) investigate whether decomposing an LLM-assisted task can improve both its outcome and the user's ability to control it. A single prompt may require several different operations, such as identifying problems in a peer review, proposing improvements, and rewriting the feedback politely. Even when a model can perform each operation separately, combining them in one call can produce incomplete results and leave users unsure where to intervene.

AI Chains treats separate model calls as building blocks. An intermediate result becomes an explicit input to another step. The system exposes these steps and their data so that users can inspect and edit the process at several levels. The contribution combines a vocabulary of primitive operations, an interactive prototype, and a controlled study of task completion. It concerns transparency of an application workflow, rather than disclosure of a model's internal reasoning mechanism.

#### Interface and interaction model

The authors survey 73 existing LLM use cases to inform operations such as ideation, classification, rewriting, and splitting or composing points. The interface connects these operations through data layers. Its Chain view shows the overall structure, while its Step view exposes the prompts, inputs, and outputs of the selected operation. Users can execute individual blocks or parallel blocks, inspect the constructed prompt, and change the content passed downstream.

![AI Chains exposes a task's connected operations and an editable view of the selected step's prompts and intermediate data. Source: Wu, Terry, and Cai (2022), Figure 3, PDF page 7; cropped from the original paper.](figures/wu2022aichains.png)

There are three principal levels of control. A user can revise a local prompt, directly edit an intermediate result, or change the chain's structure. Editing intermediate data is especially significant: it allows a user to retain useful work while correcting a local problem before it propagates. Separate calls also permit different generation settings for different purposes, such as greater variation during ideation and lower variation during translation.

This decomposition is not cost-free. The designer must decide which context each step needs, how outputs are represented, and which dependencies should be retained. An apparently clean separation may remove information that matters to a later step. The paper explicitly recognizes that strongly interdependent subtasks can lose coherence when processed independently.

#### Study design and evidence

The within-subject study includes 20 practitioners from a large software company, including designers, linguists, analysts, and technically knowledgeable non-ML engineers. Participants complete either a peer-feedback task or an English-French travel-flashcard task with both the chaining interface and a single-textbox Sandbox baseline. Interface order is counterbalanced. Both conditions use the same 137-billion-parameter LaMDA model, so the comparison changes the workflow rather than the underlying model.

Participants receive an initial tutorial and suitable starting prompts. In the chaining condition, they first work with a prepared chain while modifying prompts and intermediate content; structural modification is offered afterward. This is primarily evidence about using and adapting prepared decompositions, not a study of unrestricted chain creation from an empty canvas.

Participants rate chaining more highly for support of their thought process, control, collaboration, and transparency. Mean transparency ratings are 5.4 versus 3.8 on a seven-point scale, while control ratings are 6.2 versus 4.5. Two independent raters, blinded to condition, prefer the chaining outputs in 85% and 80% of paired comparisons. Completion time does not differ significantly in the reported analysis: approximately 14.6 minutes for chaining and 12.4 for Sandbox.

Interaction logs provide an additional behavioral result. Consecutive reruns without edits account for 51% of relevant interactions in Sandbox and 36% in chaining. Among edits, curation of existing model output rises from 41% to 77%. These observations support the claim that exposing intermediate results changed how participants worked, rather than merely increasing their reported satisfaction.

#### Observed strategies and limitations

Participants use isolated steps to diagnose failures, compare alternative paths, and retain satisfactory intermediate results. The authors describe these behaviors as a form of unit testing. The analogy is useful because the interface supports local inspection and repair, but these are human-directed checks of probabilistic text transformations rather than exhaustive software tests with formal specifications.

The study also identifies costs. Nine participants report greater complexity or a steeper learning curve. Some find it harder to predict how a local change affects the final result, and others prefer the freedom of the unstructured Sandbox during early exploration. Prepared chains can constrain users to a decomposition that does not match their own understanding of the task.

Two additional case studies explore visualization-code debugging and assisted text entry. The visualization example uses a small set of five test cases and author assessment; it illustrates feasibility rather than establishing a general debugging success rate. The assisted-entry example demonstrates branching between abbreviation expansion and phrase completion. Neither case study should be treated as equivalent in evidential strength to the controlled user study.

#### Relationship to the collection

AI Chains provides the interaction foundation for PromptChainer's subsequent authoring work. It also resembles Radhakrishnan et al.'s decomposition at the level of separate model calls. Their evaluation targets differ: AI Chains measures human experience, behavior, and task outcomes, while the decomposition paper tests sensitivity to reasoning and bias interventions. Better perceived transparency in the former does not establish causal faithfulness in the latter's sense.

For the whitepaper's research foundation, the central contribution is the editable intermediate artifact. It provides a concrete place to inspect, revise, preserve, and propagate work. Later graph and trace interfaces extend this pattern to more complex representations, but they inherit the same design problem: local control must remain understandable in relation to the full task.

### 16. PromptChainer: Chaining Large Language Model Prompts through Visual Programming

**Reviewed source:** Wu, Jiang, et al. (2022). *PromptChainer: Chaining Large Language Model Prompts through Visual Programming*.

#### Problem and contribution

Wu, Jiang, and colleagues (2022) investigate how designers and developers author their own LLM chains. AI Chains showed benefits from using prepared task decompositions, but building a new application introduces further difficulties. Outputs may have unpredictable formats, a prompt revision may change what a downstream step receives, and one faulty operation may cause errors throughout the workflow. PromptChainer addresses these problems through a visual programming environment with explicit connections, data previews, and debugging controls.

The paper is a CHI extended-abstract contribution supported by formative design work and four user case studies. Its scope is exploratory. It demonstrates that participants could construct and refine useful prototypes, while identifying authoring challenges that require further research. It does not provide a controlled comparison establishing that visual programming is faster or more reliable than coding an equivalent application.

#### Requirements and interface design

The formative work involves two software engineers and three designers over three months. Their experiences motivate three requirements: help users understand and combine LLM capabilities, manage changing input-output conventions, and trace cascading errors. These requirements concern the interfaces between model calls as much as the content of any one prompt.

The Chain View represents operations as nodes and their data connections as edges. Named input and output handles indicate how a node participates in the workflow. Status icons and inline data previews help users locate failures. The Node View supports editing and testing the selected operation, including the prompt for an LLM node or the function body for a JavaScript node.

![PromptChainer combines a node-and-edge Chain View, a selected Node View, and end-to-end execution controls. Source: Wu, Jiang, et al. (2022), Figure 1, PDF page 2; cropped from the original paper.](figures/wu2022promptchainer.png)

The node vocabulary includes generic LLM calls, LLM classifiers, evaluation and processing helpers, custom JavaScript, data inputs, user actions, and external API calls. This combination matters because realistic applications need routing, parsing, and communication in addition to text generation. The music-chatbot example classifies an utterance, follows an appropriate branch, extracts entities, queries an external service, and formats a response.

Prompt placeholders synchronize with the node's input handles. Renaming a variable in the prompt updates the corresponding connection label, reducing one source of mismatch between local editing and global structure. Example chains offer reusable patterns, including prompts whose output conventions match the available processing helpers. This is a practical form of scaffolding, although it cannot guarantee that a model will always obey the expected format.

#### Debugging and user control

PromptChainer supports independent node tests, whole-chain execution with logged outputs, and breakpoints. A user can pause execution, correct an intermediate output, and continue downstream. These operations separate diagnosis of a node from diagnosis of the complete application. They also let a developer test a downstream component without repeatedly paying for every upstream model call.

The interface therefore exposes an operational provenance structure: which output was passed into which subsequent computation. That structure is stronger evidence about application execution than a retrospective verbal account of what happened. It still does not reveal why the model produced the text within a node. The distinction links PromptChainer to the faithfulness concerns in Part I without overstating the kind of transparency it provides.

#### Evaluation and findings

Four Google participants, three designers and one developer, take part in feedback sessions. Before the session, they prepare an application idea and draft prompts for its anticipated steps. During the study, they assemble and revise their chains with the same LaMDA model used in the earlier work. All four build their intended chains, averaging 5.5 nodes. Their applications include a music chatbot, advertising descriptions, an image-query generator, and a writing assistant.

The observations reveal different authoring strategies. One participant sketches a structure using blank nodes before implementing them; others work node by node, either testing carefully or deferring detailed prompt refinement. Participants create chains both to compensate for model limitations and to make prototypes more reusable. A general ideation step followed by a classifier, for example, can be repurposed by changing the classification criterion.

Across eight chains from the study and pilot work, participants use 13 predefined helpers and four custom JavaScript nodes. This suggests that a small library of data transformations can cover many prototyping needs in the observed tasks. It does not establish that the same library is sufficient for production applications or more complex domains.

#### Limitations and research implications

The writing example exposes a loss of coherence when paragraphs are generated independently from outline points. Another case shows difficulty tracing multiple extracted entities back to their original input. These failures motivate better support for shared context, data lineage, grouping, and execution visualization. The paper also describes a participant who needed facilitator help to replace an awkward LLM-based ending operation with a simple JavaScript append. Finding an error did not always imply knowing how to repair it.

Preparation requirements may have encouraged participants to remain invested in their initial prompts and decompositions. The small, brief study also favors tasks that can be assembled within the session. The authors consequently propose support for rough chain sketches and comparison of alternative decompositions before users commit to polishing individual prompts.

PromptChainer's contribution to this collection is the transition from editable steps to an authoring environment with execution control. ChainForge later emphasizes systematic comparison across many prompts and models, while AgDebugger addresses retrospective diagnosis of agent workflows. Together, these papers suggest that an effective visual environment must support both the structure a user intends and the data that actually flow through it. A diagram alone is insufficient unless its nodes remain connected to inspectable execution evidence.

### 17. ChainForge: A Visual Toolkit for Prompt Engineering and LLM Hypothesis Testing

**Reviewed source:** Arawjo et al. (2024). *ChainForge: A Visual Toolkit for Prompt Engineering and LLM Hypothesis Testing*.

#### Problem and contribution

Arawjo et al. (2024) address the gap between trying a few prompts in a chat interface and building a custom evaluation program. Users need to compare models, prompt templates, input variations, and repeated generations. Those combinations quickly produce more responses than a person can inspect informally. ChainForge combines a visual dataflow environment with batch generation, configurable evaluation, and linked response views.

The central contribution is not simply a node-based prompt editor. It is an environment for moving between exploratory questions and explicit comparisons of model behavior. Users can formulate a hypothesis, generate the necessary variations, inspect individual outputs, and summarize results without first constructing the surrounding API and plotting infrastructure. The paper also contributes observations from laboratory users and people who had independently adopted the publicly released toolkit.

#### Visual workflow and comparison mechanisms

ChainForge organizes nodes into inputs, generators, evaluators, and visualizers. Prompt nodes can query multiple models and request repeated responses. Input variables expand into combinations of prompt values, while table-based inputs preserve associations among fields belonging to the same row. Prompt templates can themselves be nested, allowing users to compare alternative instructions and examples systematically.

![ChainForge makes an evaluation workflow visible from prompt variations and model queries through scoring and plotted results. Source: Arawjo et al. (2024), Figure 1, PDF page 1; cropped from the original paper.](figures/arawjo2024chainforge.png)

The interface retains metadata about how a response was produced. Evaluators can refer to upstream variables or associated reference answers, and users can group responses by model or prompt dimension. The Response Inspector offers a grouped list and a table layout for side-by-side reading. Visualization nodes display numerical or categorical scores, supporting an overview that can be checked against the underlying text.

Evaluation can use simple conditions, custom JavaScript or Python, or an LLM scorer. These options lower different barriers, but they do not make all criteria equally valid. A response-length measure may operationalize concision while saying little about accuracy. An LLM-based score introduces another model's judgment. The visual workflow makes the evaluation logic inspectable; the user must still decide whether that logic represents the intended question.

Caching reduces repeated requests during iteration, and previews show the number of queries a flow will produce. This is important because combinations of prompts, models, samples, and conversation histories can grow rapidly. The resulting interface problem is both computational and cognitive: users need to understand which dimensions vary and which outputs belong to each condition.

#### Evaluation design

The authors conduct an in-lab study with 21 participants and six interviews involving eight existing users. The laboratory study includes a structured email-rewriting comparison followed by open-ended investigation of a participant's own question. Participants can receive implementation assistance from the researcher. The interview study examines real uses of the interface or its source code, providing evidence beyond short, researcher-defined tasks.

The evaluation is primarily qualitative and appropriate to the toolkit's broad purpose. It asks what users can investigate, how their work develops, and where the environment creates friction. It does not establish a controlled productivity advantage over notebooks, APIs, or other prompt tools. Statements that it saved time are participant reports rather than measured comparative effect sizes.

#### Findings and modes of work

Across the studies, the authors identify opportunistic exploration, limited evaluation, and iterative refinement. Exploration involves trying prompts and revising the question itself. Limited evaluation adds explicit criteria and automated scoring, often with a small or approximate test. Iterative refinement begins once the evaluation has become sufficiently stable to guide changes. These modes are not a mandatory linear sequence; users can return to exploration when a result changes their assumptions.

In the laboratory study, participants rate the interface an average of 4.19 out of 5, and 18 express interest in using it again. Their model choices in the common email task remain divided: eight select PaLM2, seven GPT-4, and six Claude-2. This disagreement reflects differences in how participants interpret and prioritize criteria, even when they see the same responses. The system helps compare evidence without eliminating value judgments about what counts as a better output.

Real users reveal needs that are less visible in the laboratory. Five interviewees use ChainForge to prototype data-processing pipelines, with prompt selection serving a larger goal. Exporting results, sharing flows, preserving metadata, and communicating findings to colleagues become central. Some users conclude that the tested models are not reliable enough for their task, demonstrating that a useful evaluation tool need not always produce a decision to adopt an LLM.

#### Limits and relationship to the collection

Users encounter both interface friction and conceptual barriers. Connecting and arranging nodes takes effort; template variables and metadata features can be difficult to discover. Some participants create an evaluation pipeline but still test only one input, indicating that access to batch generation does not automatically produce systematic experimental design. Researcher assistance and a largely technical sample further limit claims about independent use by people with no programming background.

The paper's published system and usage findings are historical observations about the studied version. They should not be read as a current comparison of commercial products or model quality. Likewise, the prompt-injection example illustrates a limited evaluation; it is not a comprehensive security assessment.

Within Part III, ChainForge shifts attention from building one application path to comparing a space of possible behaviors. It complements PromptChainer's execution controls and LLM Comparator's analysis of paired outputs. For future reasoning interfaces, its strongest implication is to connect every aggregate judgment to the variations and examples that produced it. A visual score is most useful when users can inspect its criteria, revisit discrepant cases, and revise the evaluation itself.


### 18. Interactive Debugging and Steering of Multi-Agent AI Systems

**Reviewed source:** Epperson et al. (2025). *Interactive Debugging and Steering of Multi-Agent AI Systems*.

#### Problem and contribution

Epperson et al. (2025) study debugging when multiple LLM agents exchange messages, maintain state, and use external tools. A failure may originate in planning, delegation, a browser action, or the interpretation of an earlier result. Reading the final answer or a long transcript often does not reveal which change would repair the workflow. The paper introduces AGDebugger to support inspection, message editing, and return to earlier execution states.

The contribution combines interviews with five experienced agent developers, a debugging system, and a two-part study involving 14 additional participants. It extends the local editing controls in earlier prompt-chain tools to stateful agent teams. Its key technical and interaction requirement is that changing a past message must be accompanied by restoration of relevant agent state, rather than merely truncating a text transcript.

#### Interface and execution model

AGDebugger provides a message history, controls for sending or stepping through messages, and an overview of conversation branches. A developer can broadcast an instruction or address a particular agent, pause execution, edit a previous message, and resume from that point. The system records agent state before each message is processed. Agents expose methods for saving and restoring their state, allowing the debugger to checkpoint the team.

![AGDebugger links message inspection and editing with an overview of conversation branches created by resets. Source: Epperson et al. (2025), Figure 3, PDF page 7; cropped from the original paper.](figures/epperson2025agdebugger.png)

A reset creates a new session that shares the earlier history and checkpoints but records a separate continuation. The overview draws messages as rectangles in vertical sequences. Color can encode sender, recipient, or message type, while aligned branches make the point of intervention visible. Selecting a rectangle navigates to the corresponding message. This provides a bridge between the overall execution pattern and the text needed for diagnosis.

Checkpoint fidelity has an explicit limit. Restoring a browser's URL and viewport does not necessarily recreate all JavaScript state or a remote application's state. The system adopts an approximate restoration policy appropriate to its agents. Actions that already changed the external world may not be reversible. Consequently, a branch represents a resumed execution under the restored state, not a guarantee of an exact replay of every condition.

#### Evaluation design

The study uses a five-agent Magentic-One team implemented through AutoGen. The agents include an orchestrator, coder, executor, file browser, and web browser. Two selected GAIA Level-1 tasks require web-based information gathering and consistently produce incorrect answers in the runs selected for debugging. Their histories contain 71 and 90 messages, with more than 6,000 and 7,000 words respectively.

In the first study part, six participants inspect failures with AGDebugger and a reduced baseline in a counterbalanced design. They receive the expected and actual answers and identify errors and possible fixes. In the second part, eight new participants receive a compiled error summary and spend 30 minutes trying to steer one failing run. This separation reduces onboarding time for the steering study, but it means those participants do not independently perform the entire diagnosis-to-repair process.

The first part produces similarly high-quality error descriptions in both interface conditions. Participants spend about ten of the allotted fifteen minutes reading before beginning edits. Five of six prefer AGDebugger, largely because it supports testing a change. This is evidence of a valued interaction capability, without a demonstrated superiority in the quality of initial error identification.

#### Findings and observed interventions

In the steering study, only two of eight participants obtain the exact correct answer. All use message editing, and the reset feature receives a mean usefulness rating of 4.9 out of 5. The paper's positive usability findings should therefore be reported alongside the limited task-repair success. The system helps users investigate agent behavior even when they cannot complete the repair within the session.

The researchers classify 24 message edits into three categories: adding specific instructions, simplifying instructions, and changing the plan. Fourteen edits add detail; five simplify; five modify the plan. These strategies address different hypotheses about failure. An agent may need a more actionable instruction, a smaller immediate task, or a different approach to obtaining the information.

No participant changes the agent configuration, despite the interface supporting basic configuration edits. Participants hesitate to alter settings without understanding the implementation. Message editing is a more accessible first intervention, but even that operation requires knowledge of what an agent can do in one step. An instruction that seems reasonable to a person can exceed the receiving agent's action model.

#### Limits and relationship to the collection

Stochastic generation makes the effect of an edit difficult to interpret. A changed continuation may result from the edit, ordinary variation, or differences in the restored environment. Conversely, an edit may appear ineffective because earlier context dominates or because its consequences emerge several messages later. The authors identify repeated trials and comparison of branches as necessary directions for stronger debugging support.

The evaluation is limited to two tasks, short sessions, and technically experienced participants from one organization. It does not establish that a successful local message edit generalizes to other tasks or constitutes a durable agent-level fix. That distinction is central to connecting AGDebugger with ChainForge: an interactive repair hypothesis should eventually be tested across repeated runs and a wider set of inputs.

AGDebugger contributes a concrete intervention unit for agent oversight: an editable message tied to a recoverable execution checkpoint. Its visualization communicates observed communication history and user-created branches. It complements internal activation interventions in LM-Debugger and Patchscopes, but acts at the application level. The broader research opportunity is to connect accessible steering with evidence that a change had a reliable effect, while accurately representing what state was and was not restored.

### 19. LLM Comparator: Visual Analytics for Side-by-Side Evaluation of Large Language Models

**Reviewed source:** Kahng et al. (2024). *LLM Comparator: Visual Analytics for Side-by-Side Evaluation of Large Language Models*.

#### Problem and contribution

Kahng et al. (2024) examine how practitioners interpret automatic comparisons of two language models. A judge model can score paired responses at scale, but an aggregate win rate does not explain which prompts drive the result, what the judge rewards, or how the outputs differ. LLM Comparator connects those aggregate results with the individual prompts, responses, and rating rationales.

The system supports three related questions: when one model performs better, why the automatic rater prefers it, and how the responses differ. The word “why” has a specific scope here. It refers to rationales generated by the evaluation model, not a causal explanation of either candidate model's internal computation. Preserving this distinction is essential when placing the paper alongside the faithfulness literature.

#### Interface and visual analysis

The interface combines an interactive table with a coordinated summary panel. Each row contains a prompt, two responses, an aggregate score, and a rationale summary. Overlapping words are highlighted to support comparison. Users can open the individual ratings underlying the aggregate, including cases in which repeated judgments disagree.

![LLM Comparator links paired response inspection with score distributions, prompt-category comparisons, rationale clusters, and text-pattern analysis. Source: Kahng et al. (2024), Figure 1, PDF page 1; cropped from the original paper.](figures/kahng2024comparator.png)

The summary panel includes the score distribution and win rates by prompt category. Filtering a category updates the examples available for inspection. This supports movement from a broad pattern, such as weaker performance on a class of coding prompts, to the concrete responses that might explain it. The interface also supports the reverse direction, where an interesting example motivates a broader search.

Rationale clusters summarize recurring reasons used by the judge. Another LLM proposes representative labels from sampled rationale bullets, and embedding similarity assigns bullets to those labels. A bullet may belong to multiple clusters. Users can add or remove labels and regenerate clusters for the current subset. This makes the categorization interactive, but the labels and assignments remain model-derived interpretations of model-derived rationales.

N-gram analysis and custom functions offer complementary ways to examine the actual responses. Users can compare recurring phrases, define regular expressions, or calculate quantities such as word count. Boolean results appear as proportions and numerical results as distributions. These measurements can test whether a rationale such as greater concision corresponds to an observable pattern, while still requiring a judgment about whether that pattern is desirable.

#### Workflow and deployment evidence

The design is informed by informal conversations with more than 20 Google practitioners. Their earlier workflows relied on spreadsheets and notebooks, with substantial manual effort to connect summary metrics to long response texts. LLM Comparator is integrated with evaluation pipelines so that completed comparisons can be opened directly in the tool.

The paper reports more than 400 internal users and more than 1,000 distinct comparison experiments during its initial deployment period. Those figures establish use of the tool in an organizational setting. They do not measure improved model quality, more accurate human decisions, or productivity relative to another interface. Some deployed versions also precede the full feature set evaluated in the paper.

The observational study includes six engineers, researchers, and data scientists who had recently conducted automatic side-by-side evaluations. Each analyzes a recent evaluation from their own work during an approximately 45-minute remote session. The study therefore uses relevant work contexts, although the small sample and absence of a controlled baseline limit causal claims about interface effectiveness.

#### Findings and interpretation

The authors identify three usage patterns. In example-first analysis, participants read specific prompts and outputs, sometimes hiding the score to form an independent judgment. In prior-experience testing, they search for known undesirable patterns, such as unnecessary introductory phrases or refusals. In rationale-centered exploration, they begin with clusters or category-level differences and follow those patterns into the underlying responses.

These patterns show why coordinated views matter. A user may distrust the automatic rater, notice a possible formatting effect in one example, and then test whether that effect occurs more broadly. Another may use a rationale cluster as a starting point and discover that the judge's terminology masks several different response behaviors. The tool supports investigation of the evaluator as well as comparison of the evaluated models.

Participants request reusable definitions of unwanted patterns, richer semantic metrics, and better rationale clustering. The paper acknowledges that embedding similarity can reflect syntax as well as meaning, while generated labels and summaries can be inaccurate. In addition, summarizing only the ratings supporting the aggregate winner can suppress disagreement unless users inspect the individual judgments. The detailed rating view is therefore an important corrective to the compressed overview.

#### Relationship to the collection

LLM Comparator complements ChainForge by concentrating on analysis of already-produced paired evaluations at organizational scale. ChainForge emphasizes constructing and revising an evaluation workflow; Comparator emphasizes interpreting its results. Both demonstrate the importance of linking summaries to examples, but neither makes an automatically generated rationale inherently faithful or correct.

The system also offers a useful precedent for later visual reasoning papers. A graph or cluster should permit inspection of the original text and the transformation that produced the summary. Otherwise, compression may create a persuasive account whose uncertainties are difficult to see. Comparator's contribution is the coordinated analytical workflow, with human inspection remaining part of evaluation. Its study supports the usefulness of that workflow for experienced practitioners, while leaving controlled measurement of decision accuracy and broader adoption as open questions.

### 20. WaitGPT: Monitoring and Steering Conversational LLM Agent in Data Analysis with On-the-Fly Code Visualization

**Reviewed source:** Xie et al. (2024). *WaitGPT: Monitoring and Steering Conversational LLM Agent in Data Analysis with On-the-Fly Code Visualization*.

#### Problem and contribution

Xie et al. (2024) study oversight of LLM-generated data-analysis code. Conversational tools can produce a complete analysis from a natural-language request, but users may struggle to verify unfamiliar code or express a correction through another broad prompt. WaitGPT translates supported code operations into an interactive diagram as generation and execution proceed. Users can inspect intermediate tables, locate operations, and make targeted changes.

The paper contributes formative findings from eight users, a code-visualization and interaction design, and a twelve-participant evaluation. Its most important distinction from generic visual reasoning systems is its grounding in executable code and runtime data. The diagram represents parsed operations and observed table states, rather than relying entirely on an LLM to describe its own reasoning.

#### Representation and interaction

WaitGPT uses static analysis of Python's abstract syntax tree to identify supported operations in Pandas, Matplotlib, and Seaborn code. These include loading, selecting, filtering, sorting, transforming, grouping, aggregating, merging, adding columns, and visualizing data. The diagram contains table nodes, operation nodes, and result nodes, connected by input, assignment, sequencing, and result relationships.

![WaitGPT presents generated analysis as an interactive data-operation diagram with table-state inspection and contextual refinement. Source: Xie et al. (2024), Figure 3, PDF page 6; cropped from the original paper.](figures/xie2024waitgpt.png)

Operation nodes expose parameters, while animated table glyphs summarize changes in table dimensions. Users can open actual intermediate data and connect a diagram element to its source code. The system separates chained method calls into executable statements and inserts instrumentation to retrieve relevant runtime information. This provides evidence about what the supported operations actually did to the data.

The diagram grows during generation and execution, giving users an opportunity to monitor progress. Afterward, replay and scroll-based navigation support retrospective inspection. Users can edit operation parameters directly or ask the LLM a question in the context of a selected node. These local exchanges are kept separate from the main conversation, and modified code can be rerun using preserved execution context.

This design supplies a specific referent for a correction. A user can point to the join operation and its key column rather than describe the location indirectly in a new message. The resulting reduction in conversational ambiguity is a distinct benefit from any gain in code readability. Both depend on the diagram accurately representing the code and exposing the parameter that matters.

#### Evaluation design

The formative study finds that users often disengage while code is generated, review results afterward, and struggle with repeated conversational correction. The evaluation study then compares WaitGPT with a visually similar baseline that retains code, syntax highlighting, and comments but removes the operation diagram. Twelve postgraduate participants with varied data-analysis backgrounds complete tasks in a counterbalanced within-subject design.

The structured tasks use employee and flight data, including known errors and error-free examples. Initial responses are prepared to be identical for a given task, supporting comparison of the interfaces. A further open-ended task uses a synthesized dataset. Each structured task has six participants per interface condition, making task-level percentages sensitive to the outcome of a single participant.

#### Results and evidential limits

The task results are mixed. WaitGPT improves correctness judgments on some tasks, matches the baseline on several, and performs worse on one missing-filter task. For example, success in recognizing a sorting problem rises from approximately 33% to 83%, while a task requiring attention to an omitted employee filter falls from approximately 83% to 67%. These results support the value of exposing data and operations for some errors, but they do not show uniform improvement across error types.

Completion times also vary by task, with substantial dispersion. The table does not support a general claim that WaitGPT is faster. Some tasks take longer when participants inspect both the diagram and the code. The paper's strongest consistent findings concern subjective experience: participants report lower workload and greater usefulness for understanding, verification, correction, and engagement. Ten of twelve report increased confidence in the analysis result.

That increase in confidence must be interpreted alongside the task-level errors. The study does not establish that confidence became better calibrated to correctness. A clearer representation can make an analysis easier to follow while still failing to expose an omitted operation. This distinction connects WaitGPT directly to the whitepaper's broader concern with verification rather than perceived transparency alone.

#### Limitations and relationship to the collection

The parser supports a bounded set of languages, libraries, and code patterns. A custom lambda function may appear without enough detail to assess its semantics. The current approach does not fully address loops, arbitrary control flow, or non-tabular data, and table glyphs can become unwieldy for wide tables. Participants explicitly question whether a parameter omitted from the visualization could conceal an error.

The sample is small and more technically experienced than many intended nonprogrammer users. Participants are also encouraged to inspect the representation, which may differ from spontaneous use in everyday work. Longer deployments would be needed to determine whether monitoring persists after novelty fades and whether the display changes real verification habits.

WaitGPT contributes a grounded intermediate representation between natural-language requests and executable analysis. It complements PromptChainer's authoring of workflows and AGDebugger's intervention in message histories. For later reasoning-diagram systems, it offers an especially useful design principle: connect the visual abstraction to inspectable source operations and observed state. Its limitations also show why coverage of that abstraction must be evaluated. An interface can only help users inspect what its representation makes available.


### 21. CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities

**Reviewed source:** Lee et al. (2022). *CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities*.

#### Problem and contribution

Lee, Liang, and Yang (2022) argue that language-model capabilities in collaboration cannot be understood from isolated generated texts alone. A writer may accept a suggestion, change it, reject it but retain an idea, or use it to redirect the next paragraph. The final document hides much of this interaction. CoAuthor records the process so that researchers can examine model capabilities under different definitions of useful collaboration.

The contribution includes a writing interface, a reusable interaction dataset, a replay interface, and example analyses. The dataset contains 1,445 sessions from 63 writers interacting with four configurations of GPT-3. These are variations in decoding parameters, not four independently trained model families. CoAuthor is placed in the toolkit section because its primary contribution is an empirical resource and interface for studying human-model interaction, although its concerns also connect strongly to the sensemaking systems in Part V.

#### Dataset and interface design

The authors propose four dataset requirements: cover diverse contexts, permit multiple interpretations of good collaboration, capture processes, and support reuse and expansion. They operationalize these requirements through creative and argumentative writing tasks, twenty initial writing prompts, event-level interaction records, and post-session surveys. The collection includes 830 stories and 615 essays.

The data-collection interface resembles a text editor. Writers type freely and request five suggestions with a keyboard command. They can navigate the suggestions, accept one, dismiss the group, or continue editing. Accepted suggestions enter the document and can be revised like other text. This keeps the interface close to ordinary writing while producing a record of where the model enters the process.

![CoAuthor's text editor lets writers request, inspect, accept, dismiss, and revise model suggestions while recording the interaction. Source: Lee et al. (2022), Figure 3, PDF page 6; cropped from the original paper.](figures/lee2022coauthor.png)

The logs record text insertion and deletion, cursor movement, suggestion requests, navigation, selection, and dismissal. Events include timestamps and editor state. Deterministic event blocks then group low-level actions into interpretable sequences, such as inserting a span or selecting a suggestion. This separation preserves detailed evidence while making analysis more manageable.

The replay interface allows researchers to inspect sessions as unfolding interactions. That capability complements aggregate statistics: a numerical association can be checked against the actual sequence of user and model actions. It also allows the same dataset to support different research questions without imposing one universal label for a successful collaboration.

#### Collection and descriptive findings

The writers are recruited through Amazon Mechanical Turk after a qualification round. Sixty-two of the 63 report being native English speakers. Each session requires at least ten minutes of collaborative writing, and writers may respond repeatedly to a prompt. The resulting population and task structure provide substantial interaction data but do not represent all writers, languages, or professional writing contexts.

On average, a session contains 418 words and 11.8 requests for suggestions. The reported acceptance rate is 72.3%, while 72.6% of final text is attributed to writers. These quantities capture different aspects of collaboration: accepting one suggestion from a requested group does not mean that most final prose is machine-generated. Nor does retaining a small amount of model text imply that the model had little influence on ideas.

The example language-quality analysis compares final sentences attributed to writers, GPT-3, or both. Automated grammar checking finds fewer errors in the GPT-3 and jointly written categories than in writer-only sentences. Jointly written sentences also have higher distinct-bigram diversity. Because these are retained sentences within collaborative sessions, the result includes selection and editing effects. It is not a randomized comparison between unaided writers and a model producing complete documents independently.

#### Ideation and collaboration measures

To examine ideation, the authors track newly introduced named entities and whether writers reuse them later. In creative writing, 13% of accepted suggestions contain a new named entity, and 20% of the proposed new entities are reused in subsequent writing. Corresponding argumentative-writing figures are 7% and 14%. This is a concrete, narrow indicator of influence. It misses ideas without names, references expressed through pronouns, and inspiration from rejected suggestions.

The paper adapts equality and mutuality to event-block patterns. Equality concerns the distribution of writer and model turns; mutuality concerns the degree of interaction with model suggestions. These operational definitions make comparison possible, but they should not be treated as complete psychological measures of partnership. The analyses find substantial variation among writers and more limited variation among prompts, reinforcing the importance of individual collaboration styles.

Additional analyses connect output length with query and acceptance counts and connect perceived ownership with the proportion of writer-authored text. The paper explicitly presents these as correlations useful for forming hypotheses. It does not establish that encouraging more requests causes greater productivity or that changing text proportions causes a particular feeling of ownership. Editing frequency alone shows little association with ownership in the reported analysis.

#### Relationship to the collection

CoAuthor offers a methodological counterweight to evaluations that measure only the final answer, a satisfaction rating, or task time. A reasoning interface could similarly record which steps users inspect, challenge, modify, or leave untouched. Such records would help distinguish passive exposure to an explanation from active verification and could reveal whether a correction changes subsequent work.

The dataset also illustrates why the provenance of human and model contributions matters. An accepted statement may be edited later; a rejected statement may still affect the user's plan. Those relationships are relevant to Sensecape, iToT, and other systems where model-generated structures become part of a shared workspace. CoAuthor does not evaluate causal faithfulness of explanations, but it provides a detailed model for studying their use. Its lasting contribution is the preservation of interaction as research evidence, together with the recognition that useful collaboration has several defensible definitions.

### Part III synthesis: from visible structure to recorded intervention

These seven papers organize different stages of LLM work. AI Chains provides editable task decomposition, and PromptChainer supports authoring and debugging its connections. ChainForge constructs comparisons, while LLM Comparator helps interpret paired evaluation results. AGDebugger manipulates stateful message histories; WaitGPT exposes supported code operations and runtime data; CoAuthor preserves the sequence of human and model contributions.

Their strongest common pattern is the connection between an overview and an inspectable local artifact. Their evaluations also show that accessible controls do not automatically produce correct outcomes. A user may value a debugger without repairing the task, gain confidence without detecting an omitted operation, or build an evaluation pipeline without testing varied inputs. These distinctions establish the criteria for the next section: what does a reasoning graph represent, how is that representation produced, and what evidence shows that it helps a person understand or change the process?

## Part IV: Visualization of Reasoning Structures and Traces

The synthesis report groups five papers around explicit representations of reasoning structure. This part retains that grouping while distinguishing method diagrams, tutorial-generation trees, diagnostic dependency diagrams, retrospective trace analysis, and highlighted input references. The visual similarity of nodes and edges should not obscure their different meanings. Some edges represent execution or recorded dependency; others summarize relations inferred from generated text.

### 22. ReasonGraph: Visualization of Reasoning Methods and Extended Inference Paths

**Reviewed source:** Li et al. (2025). *ReasonGraph: Visualization of Reasoning Methods and Extended Inference Paths*.

#### Problem and contribution

Li, Shareghi, and Collier (2025) introduce ReasonGraph as a unified interface for visualizing several LLM reasoning methods and long reasoning outputs. The motivation is straightforward: a long textual response can conceal branching, refinement, and convergence that become more apparent in a graph. The system provides a common environment for selecting methods and models, viewing raw output, and examining a structured diagram.

The paper is an ACL system demonstration. It contributes an implementation and a set of method-specific visual layouts, with a brief evaluation based on ratings. Its evidence supports discussion of the system's capabilities and reported usability. It does not provide a sufficiently detailed controlled study to establish the abstract's stronger claims about reduced cognitive load or improved error identification.

#### Interface and supported representations

The interface places the query and reasoning-method controls above two columns. One column contains model configuration and raw output; the other contains visualization settings and the resulting graph. Users can choose a method manually, request a model-selected method through a meta-reasoning control, or visualize extended output from a reasoning model. Zoom, reset, and export support inspection and reuse of the diagram.

![ReasonGraph places model configuration and raw output beside a configurable visualization of the selected reasoning method. Source: Li et al. (2025), Figure 1, PDF page 3; cropped from the original paper.](figures/li2025reasongraph.png)

Six supported methods include chain-of-thought, self-consistency, least-to-most prompting, self-refinement, tree-of-thought search, and beam-search reasoning. Their layouts expose different structures. A chain is sequential; self-consistency displays multiple paths converging on an answer; least-to-most shows decomposition and successive subanswers; self-refinement shows attempts and revisions. Tree and beam layouts show alternatives and selection structure.

The beam-search example displays scored steps and highlights a selected path. These scores belong to the implemented reasoning procedure. Their presence in a graph does not establish that they are calibrated probabilities or that the selected path reflects a hidden model search. The graph represents the method's exposed outputs and organization.

For extended inference outputs, the system summarizes content into named steps and descriptions, using colors to distinguish questions, conclusions, feedback, and other elements. This can reduce the reading burden, but it introduces a summarization boundary. The raw text remains important for checking whether a node omits a qualification, merges separate statements, or gives an inferred relationship more certainty than the source supports.

#### Implementation and extensibility

ReasonGraph separates frontend visualization from backend configuration, model-provider integration, and reasoning-method modules. Mermaid renders the diagrams, while a Flask backend coordinates the requests. A common provider interface and modular reasoning methods are intended to support additional models and approaches. The paper reports integration with more than fifty models across several providers at the time of the work.

That model count is a description of the published system, not a verified current inventory. More broadly, the framework's extensibility is an implementation property that requires continued maintenance as provider interfaces and model capabilities change. The paper's architectural contribution is the separation of concerns, which makes such extension possible without redefining the visual environment for each model.

The reported parser relies on structured, properly formatted outputs. Reliability under that condition should be distinguished from robustness to arbitrary free-form traces. A system may correctly parse an XML-like structure while the generated content inside it remains incomplete or wrong. Parsing, semantic fidelity, reasoning correctness, and causal faithfulness are separate evaluation targets.

#### Evaluation and limitations

The evaluation table divides users into junior and senior categories with beginner and experienced backgrounds. It reports one-to-five ratings across functionality, accuracy, usability, aesthetics, efficiency, and potential. Average scores include 4.9 for the broad accuracy dimension, 4.75 for usability, and 4.85 for efficiency. The accuracy dimension combines text parsing, graph generation, and code implementation; it is not an observed 98% parsing success rate.

Similarly, the efficiency rating is not a measured rendering latency. The brief report provides limited detail about sample size, tasks, assignment, objective outcomes, or statistical analysis. Comparisons with plain text are reported for only some dimensions. These limitations prevent a strong inference that ReasonGraph measurably improves error detection, learning, or cognitive workload relative to text.

The paper proposes academic, educational, and development uses, including comparing methods and teaching their structures. These are plausible application scenarios rather than separately validated deployment results. Editable graph nodes are explicitly listed as future work. The reviewed implementation should therefore not be described as already supporting direct modification of reasoning through node editing.

#### Relationship to the collection

ReasonGraph provides a useful bridge from the workflow tools in Part III to the reasoning-specific systems that follow. It makes structural differences among prompting and search procedures visible in one environment. Unlike BertViz or AttentionViz, it operates on explicit reasoning outputs rather than attention tensors. Unlike AGDebugger, its principal contribution is visualization rather than checkpointed execution control.

Its research value lies in this representational breadth and in the availability of raw output beside the graph. The remaining question is whether the visualization supports reliable human judgments about the content. Later papers in this part can be compared against that question through their treatment of source links, hierarchy, editing, and evaluation. ReasonGraph demonstrates a workable presentation framework; the evidence required to establish semantic fidelity and effective human verification remains a separate undertaking.


### 23. SPROUT: An Interactive Authoring Tool for Generating Programming Tutorials with the Visualization of Large Language Models

**Reviewed source:** Liu et al. (2025). *SPROUT: An Interactive Authoring Tool for Generating Programming Tutorials With the Visualization of Large Language Models*.

#### Problem and contribution

Liu et al.'s SPROUT addresses programming-tutorial authoring with LLMs. A tutorial must explain the supplied code accurately while meeting an author's preferences for structure, audience, and detail. Repeated chat prompts can produce useful prose, but they make it difficult to preserve context, compare alternatives, or determine which code a paragraph describes. SPROUT turns tutorial generation into a sequence of visible, editable decisions.

The local PDF is the October 2024 arXiv revision, while the final journal publication is dated 2025. The review follows the local paper's methods and evidence and uses the final publication in the reference list. The apparent 2021 dates in the PDF's LaTeX template are placeholders, not the publication date.

The contribution combines an LLM-driven authoring procedure, six coordinated interface views, a technical test of text-code connections, and a user study. The paper uses “faithfulness” principally to mean consistency of tutorial content with source code. This differs from causal faithfulness of an explanation to the model's internal computation, as discussed in Part I.

#### Generation and visual controls

The prompting strategy combines observation, thought, and action with a tree of alternative next steps. Available actions write a title, background, code explanation, notification, or summary. At each stage, the agent considers the source code and current tutorial, proposes alternatives, votes on a next action, and retains the alternatives for later exploration. Human instructions can enter between steps to guide generation, organization, or refinement.

The Code and Tutorial views display the two principal artifacts. A Chain view connects selected tutorial paragraphs with their associated code. The Outline view shows the tree of generation steps, the Branch view exposes alternative continuations and their stated reasons, and the Node Space view supports comparison and rewriting of paragraph alternatives.

![SPROUT coordinates source code, tutorial text, paragraph-code links, and views for exploring and editing alternative generation paths. Source: Liu et al. (2025), Figure 3 in the reviewed arXiv revision, PDF page 7; cropped from the original paper.](figures/liu2024sprout.png)

Authors can begin with automatic generation or select a code region for targeted explanation. Grouping nodes condenses paragraphs, splitting a node elaborates content, and trimming removes unwanted content and descendants. Branches preserve earlier alternatives. Selecting a node as a chain endpoint assembles its ancestor path into a tutorial, while stepwise selection supports more deliberate construction.

Node Space projects paragraph embeddings into two dimensions with UMAP and highlights alternatives associated with the same action and code fragment. It supports selection by semantic similarity, writing style, and level of detail. The projection is an aid to finding alternatives, not a correctness measure. Likewise, branch widths encode the agent's votes, and edge text contains its stated reasons; neither is an independently validated probability that a tutorial path is reliable.

#### Source linkage and technical evidence

The model is prompted to return structured fields identifying the paragraph, a code excerpt, an explanation, and a brief summary. String matching then connects the returned excerpt to the source code. This creates explicit navigation between text and code, but the semantic choice of the relevant excerpt remains model-generated. The linkage mechanism is therefore different from WaitGPT's static parsing of executable operations.

The technical evaluation uses ten code snippets with varied languages, lengths, and structures. Three experienced programmers establish reference connections for 138 generated paragraphs. SPROUT produces 119 correct links and 19 erroneous ones, yielding 86.2% accuracy in that sample. Twelve failures concern an incorrect code range, five omit a code reference, and two provide code content that does not match the source.

This result measures linkage accuracy, not the correctness of every explanation or the educational quality of complete tutorials. The errors also matter operationally: an overbroad range can make a paragraph appear supported without identifying the particular operation it explains. A user may need to verify the link before using it to verify the prose.

#### User study and findings

The twelve-participant study compares SPROUT with a baseline containing a document editor, code viewer, and ChatGPT. Tool order is counterbalanced. Six participants are experienced tutorial authors from the formative study, and six have documentation experience without prior tutorial-authoring experience. All have more than four years of programming experience. A targeted task is followed by open-ended exploration in SPROUT.

Participants rate support for generating and modifying tutorial content more highly with SPROUT. Mean modification-support ratings are 4.42 versus 3.00 on a five-point scale, with a reported p-value of .007. Ease of use also favors SPROUT. Participants use automatic generation as a starting point, switch branches to compare structures, and make local refinements through the graph and paragraph controls.

Several other differences are not statistically significant in the reported study. Comprehension ratings have p=.157, confidence p=.070, and satisfaction with overall tutorial quality p=.317. These outcomes should not be restated as demonstrated improvements in comprehension, confidence, or tutorial quality. They are favorable descriptive ratings with limited statistical support in this sample.

#### Limitations and relationship to the collection

The evaluation does not measure learner outcomes in an educational deployment. It also combines a new prompting strategy with a richer interface, making it difficult to attribute benefits to a single feature. Reuse of formative participants may influence familiarity and expectations. Long code and tutorials introduce context and navigation limits, while merging content across distinct branches remains future work.

SPROUT belongs in this section because the generation tree is a central object for authoring and revision. It also connects directly to CoAuthor's interest in human-model contribution and PromptChainer's editable intermediate artifacts. Its strongest contribution is the ability to manipulate tutorial structure while maintaining visible code references and alternative versions. The technical and user evidence support that workflow, while leaving semantic correctness, causal faithfulness, and educational effectiveness as distinct questions.

### 24. When the Chain Breaks: Interactive Diagnosis of LLM Chain-of-Thought Reasoning Errors

**Reviewed source:** Chen et al. (2026). *When the Chain Breaks: Interactive Diagnosis of LLM Chain-of-Thought Reasoning Errors*.

#### Problem and contribution

Chen et al. (2026) introduce ReasonDiag for diagnosing long reasoning traces containing factual mistakes, logical gaps, uncertainty, and self-correction. A reader may identify a suspicious sentence but struggle to determine which premises support it or whether it affects the final answer. ReasonDiag combines automated error detection with linked visualizations of step roles, premise dependencies, and diagnostic evidence.

The contribution focuses on diagnosis rather than correction. It includes a nine-person formative study, an error-detection pipeline, a visual analytics interface, a technical evaluation, and interviews with sixteen users. The system treats automated judgments as candidates for human review. That orientation is important because the detector favors recall and produces many false positives.

#### Pipeline and evidential basis

ReasonDiag segments a trace into sentences, classifies their functional roles, assesses which contain checkable claims, and uses an LLM to identify premise-conclusion relationships. Roles include planning, fact retrieval, computation, uncertainty management, consolidation, checking, and answer emission. The resulting dependency structure supports both navigation and analysis of downstream consequences.

Factual checking uses retrieval through Loki to gather supporting, refuting, or irrelevant evidence. Missing or conflicting evidence is flagged for review under the recall-oriented policy. A flagged claim therefore does not always mean that external evidence has established its falsity. This distinction should remain visible to anyone using the interface to make a correctness judgment.

Logical checking translates natural-language premises and conclusions into symbolic expressions and then executable Z3 code. The solver evaluates the resulting formal constraints. Its guarantees apply to the encoded problem, while the selection of premises and translation from language remain fallible model operations. The paper's prose also does not fully specify the solver query needed to distinguish entailment from inconsistency; an unsatisfiable result must be interpreted relative to the exact formula checked. The review therefore treats this as a hybrid diagnostic pipeline, not a formal guarantee for unrestricted natural-language reasoning.

#### Interface and visual semantics

The Overview places steps along an ordinal axis, with role markers, error indicators, forward arcs for propagated flags, and backward links for uncertainty references. Filters support selection by step type and graph-derived importance. A hierarchical Section View groups steps under summaries, shows premise relationships, and allows inspection of diagnostic evidence. The original trace remains available in step or section form with linked navigation.

![ReasonDiag combines an overview of step roles and propagated error flags with hierarchical dependencies, diagnostic evidence, and the original trace. Source: Chen et al. (2026), Figure 2, PDF page 6; cropped from the original paper.](figures/chen2026reasondiag.png)

The design distinguishes a step's local status from its dependence on a flagged premise. A step can appear locally acceptable while retaining a warning about an upstream dependency. Selecting it exposes relevant premises and downstream uses. This makes the interface useful for investigating why a final statement is suspect, provided the inferred dependency graph is accurate.

Those edges describe dependencies reconstructed from the text. They are not experimentally measured causal links inside the model. Similarly, uncertainty markers describe language in the trace rather than a calibrated estimate of model uncertainty. These distinctions connect ReasonDiag to both the faithfulness literature and Kuhn et al.'s technically different meaning-level uncertainty measure.

#### Technical evaluation

The authors annotate thirteen traces from DeltaBench, comprising 2,030 sentences and 1,171 verifiable statements. A ten-person annotator pool contributes labels, with disagreements resolved through discussion and author adjudication. The comparison uses GPT-5 for ReasonDiag and two prompt-based baselines.

ReasonDiag reports recall of 0.801, precision of 0.306, and F1 of 0.386. The stronger prompt baseline has recall of 0.658, precision of 0.432, and F1 of 0.470. ReasonDiag therefore finds more labeled errors while generating more false alarms and achieving a lower F1 score. The result supports its stated recall-oriented design, rather than an unqualified claim of superior error detection.

The appendix attributes 44.48% of its false positives to propagation. In some traces, an early factual-checking mistake causes a long sequence of downstream flags. The visualization may help users trace those flags to a small number of originating claims, but the paper does not quantify whether this fully offsets the additional verification burden. It is a design rationale supported by examples, with a practical cost that remains to be measured.

#### User evidence and limitations

Sixteen university participants with varied disciplinary backgrounds inspect two cases after a walkthrough and free exploration. They report favorable ratings for locating errors, understanding sections, and using the interface. The study includes illustrative cases involving arithmetic and a multi-hop factual query. It does not include a controlled plain-text condition or objective comparative measures of diagnostic accuracy and time, despite broader comparative language elsewhere in the paper.

Participants identify dense links as a readability problem and note that finding a suspicious node does not remove the need to reconstruct the argument. They request finer distinctions among missing evidence, contradictory evidence, and logical errors, as well as future editing support. These requests reinforce the difference between localization and explanation of an error.

ReasonDiag advances the collection by placing diagnostic evidence and dependency tracing in one interface. It offers more explicit checking than ReasonGraph and a different task from SPROUT's authoring. Its strongest research implication is that error flags should be inspectable, attributable, and revisable. The technical results also show why that principle matters: a clear display of an imperfect detector can support review, but it cannot turn the detector's judgments into established facts.


### 25. ReTrace: Interactive Visualizations for Reasoning Traces of Large Reasoning Models

**Reviewed source:** Felder et al. (2026). *ReTrace: Interactive Visualizations for Reasoning Traces of Large Reasoning Models*.

#### Problem and contribution

Felder et al. address the difficulty of understanding long, explicit reasoning traces. Reading such a trace linearly can obscure the model's repeated attempts, verification, and return to earlier assumptions. ReTrace restructures the displayed trace into phases and subphases so that a reader can inspect both its overall organization and its original text. Its contribution is a taxonomy, two alternative visualization designs, and a comparative user study.

The reviewed file is the November 2025 arXiv manuscript, which contains unfinished ACM publication fields. The reference list identifies the subsequent 2026 publication. This distinction matters because the local manuscript, rather than a silently substituted publisher version, supplies the methods and numerical results summarized here.

ReTrace explicitly distinguishes an observable reasoning narrative from the full internal computation of a language model. Its visualizations describe the former. They do not establish that the narrative faithfully records the hidden causes of the answer. Within that boundary, a trace remains a useful artifact for examining stated approaches, explicit checking, and repetition.

#### Structuring and displaying a trace

The pipeline uses an external language model to organize a DeepSeek-R1 trace. It first indexes text segments, obtains a structured classification, and then reinserts the original indexed text. This design helps preserve the wording of the source while allowing generated labels and summaries to support navigation. It does not eliminate classification errors: a correctly copied sentence can still be placed under an incorrect phase or described by an inaccurate summary.

The taxonomy has four main phases: problem definition and scoping; initial solution development and exploration; iterative refinement and verification; and final decision. Twelve subtypes distinguish activities within those phases. Consecutive steps are grouped together, preserving the temporal order of the written trace rather than collecting every occurrence of a category into a single disconnected bin. Iterative refinement is optional because not every trace contains it.

Four experts informed the design process. The authors considered a node-link representation but dropped it because crossing links and layout complexity impeded reading. The two retained designs provide different ways to move between global structure and detailed text.

![ReTrace's Space-Filling view organizes a reasoning trace into phase regions and supports drilling down to subphases and the original text. Source: Felder et al. (2026), Figure 4 in the reviewed manuscript, PDF page 10; cropped from the original paper.](figures/felder2026retrace-space.png)

The Space-Filling view begins with four phase regions arranged in two columns. Their initial sizes do not encode the number of reasoning steps. Separate indicators report the distribution of steps, and readers can expand a region to inspect subphases and source passages. The layout supports an overview of the kinds of activity represented in a trace.

The Timeline view places successive phase groups from left to right. Width represents step count, not execution duration. Expanding a phase reveals progressively finer detail. It therefore emphasizes sequence and recurrence, while the Space-Filling view emphasizes the division of activity among phases. Neither view supplies checkpoint restoration or direct steering of the generator.

#### Evaluation and findings

Eighteen participants used the Space-Filling view, Timeline view, and raw text in a counterbalanced within-participant study. Eleven had computing or engineering backgrounds. The materials comprised three traces: one each from DROP, GSM8K, and a Zebra puzzle. These provide contrasting examples but are not a representative sample of reasoning tasks or model behaviors.

Participants summarized traces, identified verification behavior and confidence-related points, estimated the share devoted to verification, and judged answer correctness. The researchers also collected task time, perceived ease, workload, and preferences. The visual interfaces displayed the same underlying trace content as the raw-text condition, while adding labels, summaries, and quantitative indicators. Consequently, the experiment evaluates a package of structural annotation and visualization. It does not isolate the effect of spatial layout from the effect of generated summaries.

![ReTrace's Timeline view preserves the sequence of phase occurrences and progressively reveals their contents. Width represents the number of steps, not measured elapsed time. Source: Felder et al. (2026), Figure 5 in the reviewed manuscript, PDF page 11; cropped from the original paper.](figures/felder2026retrace-timeline.png)

The visual conditions produced higher descriptive summary scores: their median was 1.5 on a zero-to-two scale, compared with 1 for raw text. Median counts of identified verification types were also higher. However, performance differed by task. Thirteen participants identified the designated confidence point with Space-Filling, eleven with raw text, and eight with Timeline. The findings therefore do not support a uniform advantage for every visual representation and every interpretation task.

The median absolute error in estimating the verification share was about 0.30 percentage points in both visual conditions, compared with 14.6 for raw text. The Space-Filling comparison with raw text was statistically significant. This is useful evidence that the display communicates its computed distribution, but that distribution is directly available in the interface. It should not be interpreted as an independent test of whether participants accurately classified verification steps themselves.

Timeline received a higher median ease score than raw text, and Space-Filling produced significantly lower reported workload than raw text. There was no significant completion-time difference. Eleven participants preferred Space-Filling, six preferred Timeline, and one preferred raw text. Answer-correctness judgments were already near ceiling: seventeen of eighteen were correct with raw text and Space-Filling, and sixteen with Timeline. Those results do not establish improved detection of difficult reasoning failures or calibrated trust.

#### Interpretation and relationship to the collection

ReTrace provides evidence that structured views can reduce perceived effort and support some forms of trace summarization and navigation. Its strongest contribution is the explicit comparison of two representational choices against raw text. Its limits include the small trace set, static presentation, dependence on generated segmentation, and the absence of a difficult error-detection task.

Compared with ReasonDiag, ReTrace organizes the activities described in a trace rather than deriving a graph of premises and suspected errors. Compared with ReasonGraph, it studies alternative layouts and human interpretation in greater depth. Compared with AGDebugger, it supports retrospective reading without restoring execution state. Future work could connect these capabilities, but the present study should not be read as evidence for real-time intervention or guaranteed understanding of the model's internal reasoning.

### 26. HoT: Highlighted Chain of Thought for Referencing Supporting Facts from Inputs

**Reviewed source:** Nguyen et al. (2026). *HoT: Highlighted Chain of Thought for Referencing Supporting Facts from Inputs*.

#### Problem and contribution

Nguyen et al.'s HoT makes references between input facts and reasoning text visible through matching highlights. The abbreviation means **Highlighted Chain of Thought**. It does not refer to hierarchical reasoning. The paper combines a prompting procedure, a lightweight visual component, benchmark experiments, ablations, a human study, and small-model fine-tuning experiments.

The reviewed local file is the June 27, 2026 arXiv revision associated with publication in Transactions on Machine Learning Research. Its principal idea is to ask the model to repeat relevant input content with numbered fact tags and reuse those tags when the answer draws on the corresponding facts. A renderer then applies matching colors. This creates an explicit reference mechanism that can be inspected without a separate graph interface.

The contribution has two distinct questions. One is whether producing tagged references improves model answers. The other is whether displaying the resulting highlights helps people judge those answers. The paper investigates both, and its findings make it particularly important to keep generation quality separate from human verification.

#### Prompting and visual reference mechanism

The prompt asks the model to wrap facts in XML-style tags such as numbered fact elements and to reuse the identifiers in its response. Regular expressions and CSS transform these tags into consistent highlights. A reader can associate a reasoning passage with the input fact that shares its color. The visible linkage can reduce the effort of searching back through a question or document for supporting information.

![HoT uses matching highlights to connect facts in the input with passages in the generated reasoning. These are model-assigned references, whose correctness still requires checking. Source: Nguyen et al. (2026), Figure 3, PDF page 5; cropped from the original paper.](figures/nguyen2026hot.png)

The evaluated prompting procedure uses task-specific demonstrations. The preparation process begins with human-authored examples and uses model assistance to construct demonstration material. It is therefore more specific than a universal instruction that can be added to any task without preparation. The model must also follow a structured output format, which can be difficult for smaller models and long inputs.

Repeating the input and adding tags changes the generation context. HoT is consequently both a prompting intervention and a display technique. Its model-performance gains cannot be attributed solely to the colors shown to a human reader. Conversely, the presence of a matching color does not prove that the linked input entails the associated claim. The model assigns the references and can attach an inappropriate source fact to a plausible-looking step.

#### Model experiments and limitations of the measures

The benchmark program spans twenty-two tasks and several models, including Gemini, Llama, and GPT-4o variants. Coverage varies across experiments; the paper should not be read as testing every model on every task under one complete factorial design. Reported averages favor HoT across several task families, with gains of roughly two to three percentage points in the principal arithmetic, question-answering, logic, and long-context groupings. Individual task results vary, and the method does not improve every condition.

An inconsistency in one table's arithmetic baseline average makes the larger aggregate improvement reported for that condition unsuitable as a clean headline result. The broader conclusion is that explicit fact tagging is promising under the evaluated prompts, not that a single large improvement applies uniformly across models or tasks.

The paper also reports a lower SelfCheckGPT score for HoT. This score concerns consistency among sampled statements and should not be equated with a directly measured factual-error rate. Consistently repeated false statements can receive favorable consistency scores. A further model-based span assessment flags contradictions, missing context, mathematical mistakes, and logical errors, but remains dependent on an automated judge. These analyses support further investigation rather than proving that the output has become reliably truthful.

The ablations examine repetition, tagging in the question, tagging in the answer, and alignment of the tags. Interpretation is complicated when models do not obey an ablated instruction and produce additional tags anyway. Deliberately misaligned demonstrations reduce performance, suggesting that the correspondence carries useful information, while still leaving open how much comes from repetition, formatting, or task-specific examples.

Fine-tuning experiments on small Llama and Qwen models use 3,187 generated examples and evaluate transfer to additional tasks. The reported results favor HoT training over the corresponding baselines in those settings. Lower measured attention entropy accompanies the tagged format, but this observation is not a causal demonstration that a particular attention change explains the accuracy gains. Training data, formatting, and task transfer remain part of the experimental package.

#### Human evaluation: speed and incorrect-answer acceptance

The human study involved sixty-three undergraduate and graduate students, each making ten correctness judgments. Participants were assigned to highlighted or unhighlighted presentations. Crucially, the unhighlighted condition removed tags from the same HoT-generated text. This holds the wording constant and tests the presentation effect more directly than comparing separately generated CoT and HoT answers would.

The stimulus pool contained sixty correct and sixty incorrect answers drawn from DROP and GSM-Symbolic. Each had a highlighted and an unhighlighted display version. Participants had a two-minute limit per judgment. The reported mean judgment time fell from 62.38 seconds without highlighting to 47.26 seconds with highlighting, a reduction of about twenty-four percent.

The correctness results reveal an important tradeoff. Participants accepted correct answers more often with highlights: 84.48 percent versus 78.82 percent. However, they rejected incorrect answers less often: 54.83 percent versus 72.21 percent. Highlighting therefore improved speed and acceptance of valid answers while substantially impairing recognition of invalid answers in this study. A claim that HoT simply improves human verification would omit its most consequential adverse result.

The practical value of that tradeoff depends on the frequency of incorrect answers and the relative costs of false acceptance and false rejection. The balanced experimental pool does not establish those quantities for deployment. Nor does faster judgment by itself establish better understanding or appropriate trust.

#### Relationship to the collection

HoT supplies a compact interface component that could be incorporated into tools throughout Parts III and IV. Unlike ReTrace's phase summaries, it links claims to input spans. Unlike a citation to an external source, the link is generated within the prompting procedure and requires its own validation. Its human study provides a direct warning against using visual coherence as a substitute for evidence: a display can make an answer easier to follow while making its errors easier to accept.

### Synthesis of Part IV

These five papers operate on explicit reasoning or authoring artifacts, but their objects and controls differ. ReasonGraph renders the structure of multiple reasoning procedures. SPROUT exposes alternatives while constructing a programming tutorial. ReasonDiag derives dependencies and flags possible errors. ReTrace organizes a completed trace into navigable phases. HoT links input facts to generated passages through highlights.

The common research question is whether making structure visible helps a person perform a particular task. The appropriate answer depends on the task: authoring, summarization, diagnosis, source checking, or correctness judgment. Evidence for one cannot automatically support another. ReTrace's workload reduction, SPROUT's authoring results, ReasonDiag's recall-precision tradeoff, and HoT's impaired rejection of incorrect answers illustrate why a single label such as “better interpretability” is insufficient.

An effective next study would separately evaluate source preservation, the correctness of generated structure, the reader's ability to detect errors, and the consequences of any intervention. The interfaces in this part provide useful design candidates. They also make clear that visual organization is itself a transformation whose assumptions and failure modes need to remain inspectable.


## Part V. Human Interaction, Sensemaking, and Reasoning Verification

The source synthesis report groups these four papers around human participation in working with LLM information and reasoning. That grouping is retained here. Sensecape supports exploration and organization; iToT supports selection and insertion of candidate thoughts; Hippo supports review and revision of a topical reasoning hierarchy; and Zhou et al. test interactive formats for verifying mathematical explanations. Together they connect interface operations with the different human tasks those operations are intended to support.

### 27. Sensecape: Enabling Multilevel Exploration and Sensemaking with Large Language Models

**Reviewed source:** Suh et al. (2023). *Sensecape: Enabling Multilevel Exploration and Sensemaking with Large Language Models*.

#### Problem and contribution

Suh et al. address the mismatch between a linear conversation and the nonlinear work of exploring a complex subject. A person preparing a presentation or investigating a possible move may need to pursue several topics, revisit earlier material, compare alternatives, and organize a developing understanding. A chat history preserves the order of conversation but does not necessarily preserve the organization of the problem.

Sensecape combines an LLM with a canvas and a hierarchy of topic canvases. Its central contribution is the external representation of levels of abstraction. Users can work within a topic, move into its details, and return to a broader view that shows how the topics relate. The design draws on information foraging and sensemaking: gathering material and organizing it are interleaved activities rather than separate phases that must take place in different applications.

The paper identifies six practical difficulties: deciding where to begin, revisiting information, creating structure, managing information volume, avoiding visual clutter, and switching between collection and organization tools. These difficulties explain the interface choices more precisely than a general claim that graphical interfaces are better than chat.

#### Canvas, hierarchy, and semantic navigation

The canvas is an infinite whiteboard on which users create, group, connect, and arrange text nodes. A selected node offers commands to prompt the model, request an explanation, generate questions, or suggest subtopics. A user can extract a passage from a generated response into its own node and continue exploring from it. This keeps the object being investigated close to the operation that acts on it.

![Sensecape connects a local canvas with a hierarchy of topic canvases, allowing users to organize information and navigate among levels of abstraction. Source: Suh et al. (2023), Figure 1, PDF page 1; cropped from the original paper.](figures/suh2023sensecape.png)

Semantic zoom changes the amount of text shown as the user zooms. The interface can display the full response, summaries of its lines, a paragraph summary, or keywords. These shorter forms are generated by the LLM. They support overview and navigation but can omit qualifications or introduce summarization errors; the full source response remains necessary for detailed inspection.

Semantic dive creates a lower-level canvas from a selected topic. The original node becomes a portal into that space, and the hierarchy view records the relationship. Users can also add broader topics, sibling hierarchies, and custom or generated subtopics. The hierarchy uses a restrained three-dimensional presentation intended to avoid overlapping canvases and severe perspective effects.

The evaluated implementation used GPT-3.5 Turbo for conversational generation and GPT-4 for other language-based functions. The choice reflected the authors' contemporaneous balance of response speed and instruction following. These are implementation conditions of the study, not a recommendation about current models.

#### Comparative study and findings

Twelve participants completed a within-participant comparison using two complex topics: AI's effect on the future of work and global warming's economic effects. Each task lasted twenty minutes, and interface and topic order were counterbalanced. Participants prepared material as though they would later give a talk and share their organization with colleagues.

The baseline integrated a chat panel with a diagramming canvas and allowed easy transfer of highlighted text. This is an important design detail. The study did not compare Sensecape only against a bare chat window or a laborious copy-and-paste workflow. It tested the additional hierarchy and semantic-navigation capabilities against an already integrated collection-and-notes environment.

Participants issued similar numbers of prompts and created similar numbers of nodes and connections in the two conditions; those differences were not statistically significant. They did, however, record more unique domain concepts with Sensecape: a mean of 68.3 compared with 22.8. Two raters coded concept coverage using domain glossaries. This supports broader represented coverage within the study period, while not establishing that every concept was accurate or understood.

The resulting knowledge structures had more hierarchical levels with Sensecape, averaging 4.3 versus 2.6. Participants also revisited previously encountered information more often, averaging 12.8 revisits versus 0.7. These behaviors are consistent with active organization and reconsideration. Hierarchy depth is nevertheless partly encouraged by the interface itself and should not be treated as an independent measure of learning quality.

Participants commonly valued semantic zoom, semantic dive, and the hierarchy view. Seven generally preferred Sensecape, and nine preferred it for gaining a deeper understanding. Preferences for broad exploration were more divided. Some found the hierarchy useful for maintaining context, while others found the added spatial and conceptual controls demanding. The study therefore identifies a task-dependent tradeoff between representational power and learning effort.

#### Limits and relationship to the collection

The evaluation measures exploration behavior, external organization, and perceived usefulness. It does not establish durable learning, factual correctness, or better decisions. The brief sessions and small sample also leave long-term use unresolved. Participants proposed collaborative uses, but collaboration was future work rather than an evaluated capability of the implementation.

Fact checking was deliberately omitted from the study system. The authors explain that adding source verification would have changed the experience they were studying. This is a substantial boundary for academic information work: Sensecape can organize generated information without establishing that the information is supported by external sources.

Within this collection, Sensecape provides a foundation for multilevel information organization. ReTrace applies related overview-and-detail concerns to completed reasoning traces, while Hippo applies hierarchical presentation to editable reasoning. ChainForge instead organizes experimental comparisons. Sensecape's research value is the connection between information structure and exploration behavior. A future literature-work interface would need to add reliable document provenance and evidence checking before interpreting a well-organized canvas as a well-supported synthesis.

### 28. iToT: An Interactive System for Customized Tree-of-Thought Generation

**Reviewed source:** Boyle et al. (2024). *iToT: An Interactive System for Customized Tree-of-Thought Generation*.

#### Problem and contribution

Boyle et al. turn Tree-of-Thought prompting into an interactive web interface. The motivating problem is that a programmatic search procedure can generate alternatives and evaluate them without giving the user an accessible way to inspect the alternatives, supply a missing idea, or adapt the process to a new task. iToT exposes candidate thoughts, model-assigned rankings, and user-selected paths in a tree.

The paper contributes a general task-configuration interface, incremental tree exploration, and semantic grouping of similar candidate thoughts. Its evidence consists of three illustrative use cases. It does not report a controlled participant experiment or a benchmark establishing that users solve a broad set of tasks more accurately or quickly.

The system is relevant to three proposed user groups: people seeking a useful answer, practitioners configuring a prompting strategy, and researchers investigating that strategy. These are design targets. The use cases demonstrate possible workflows rather than validating effectiveness separately for all three populations.

#### Configuration and incremental generation

A user provides the main task prompt, an example of a successful thought sequence, and criteria for evaluating candidate thoughts. The example and evaluation prompts are editable parts of a more general prompting framework. Defaults reduce the initial setup burden, but the paper emphasizes that their suitability matters, especially for tasks with strict constraints.

Some settings are fixed when a tree is initialized, including temperature and generation, grouping, evaluation, and selection methods. Other settings can change during exploration, such as the number of thoughts generated or displayed at a layer. This distinction prevents the interface from being described as permitting arbitrary changes to every aspect of an existing tree.

![iToT displays ranked candidate thoughts, a model-preferred path, the user's active path, collapsible branches, and controls for inserting a custom thought. Source: Boyle et al. (2024), Figure 4, PDF page 4; cropped from the original paper.](figures/boyle2024itot.png)

The main view is a zoomable node-link tree. A green path indicates the model's preferred continuation, while a yellow path indicates the user's active exploration. Users expand a selected thought to generate continuations and collapse subtrees to manage the growing display. A custom thought can be inserted alongside generated candidates, after which the system generates children for the new contribution.

The model evaluates candidates individually or comparatively. The interface can select displayed candidates greedily by those evaluations or through random sampling. These rankings describe the model's assessment under the configured prompt. They are not independently established correctness scores, and the paper's own mathematical example shows the preferred candidate being wrong.

Semantic grouping reduces repeated options. The implementation offers sentence-embedding similarity and an NLI-based alternative using auxiliary models. Similar candidates appear as a stack that the user can expand. Grouping can help a reader identify repeated ideas, but an embedding threshold or entailment classifier can also merge distinctions that matter to the task. Inspectable grouped contents are therefore important to the design.

#### What the cases demonstrate

The vacation-planning case shows preference-based steering. The user supplies a prior trip as an example, inspects proposed activities, and inserts a planned activity that the model did not choose. Later suggestions incorporate that intervention. The case demonstrates the mechanics of altering a path without restarting the entire interaction. It does not independently verify travel facts or compare the resulting itinerary against another planning method.

The mathematical case concerns proving that the complement of a disconnected graph is connected. The model initially prefers an incomplete approach that considers only some vertex pairs. The user selects the stronger alternative and later inserts a request to address a missing part of the proof. The model then elaborates the argument. This example makes the value of an override concrete: the user can act on knowledge that the model's ranking failed to apply.

The third case revisits the proof to examine evaluation prompts. A loosely phrased preference for using more of the graph fails to select the desired approach, while wording the criterion in terms of global versus local reasoning succeeds in the example. The interface makes this prompt sensitivity observable. A systematic experiment would still be needed to establish whether that wording generalizes beyond the displayed case.

Together, the cases show configuration, selection, insertion, and comparison. They are not three independent controlled studies of co-writing effectiveness. The distinction matters because the paper's broader claims about quality, transparency, and generality are supported primarily by implemented functionality and examples.

#### Limits and relationship to the collection

The authors note API latency, dependence on suitable examples and evaluation criteria, and differences in structured-output compliance across the available GPT models. Generation-status messages and onboarding examples address some usability costs. Automatic extension of an entire preferred path is explicitly future work: in the reviewed system, each layer is generated through user action.

The discussion treats semantic agreement as a possible cue to consistency. As Kuhn et al. show more formally, meaning-level variation can inform uncertainty estimation, but repeated agreement does not establish truth. iToT's stacks and rankings should therefore be interpreted as evidence about generated alternatives, not as calibrated confidence displays.

iToT differs from ReasonGraph by providing an explicit action on the developing tree, and from PromptChainer by representing candidate continuations rather than a reusable data-processing workflow. It is close to SPROUT's exploration of authoring alternatives, although SPROUT adds a specialized tutorial task and comparative evaluation. The central research opportunity is to test whether users can use the available controls to detect and correct failures, including cases where the model's preferred path and semantic grouping are misleading.

### 29. Interactive Reasoning: Visualizing and Controlling Chain-of-Thought Reasoning in Large Language Models

**Reviewed source:** Pang et al. (2026). *Interactive Reasoning: Visualizing and Controlling Chain-of-Thought Reasoning in Large Language Models*.

#### Problem and contribution

Pang et al. introduce Interactive Reasoning and implement it in Hippo. The system presents a long reasoning trace as a topical hierarchy that users can inspect and edit before generating an updated response. Its motivating setting is a decision involving personal context and uncertain tradeoffs, where a generic answer may omit considerations that matter to the user.

The local PDF is the June 2025 arXiv manuscript; the collection associates the work with its 2026 publication record. The methods and results here come from that local version. The paper combines an interaction design, a pipeline for restructuring and linking text, a sixteen-participant study, and two follow-up cases.

Hippo's central move is to make intermediate text an editable input to subsequent generation. It does not expose or edit the model's hidden activations. The paper also explicitly acknowledges that its displayed links between reasoning and response are semantic associations rather than causal relationships inside the model.

#### Representation and intervention

The interface progressively displays a tree in preorder, moving from a parent topic into its subtopics. Users can pause the presentation, edit a node, add a branch through a custom prompt, delete a node or subtree, and regenerate content. A feedback node interrupts progression when the system identifies a point where the user's context or preferences may be useful.

![Hippo presents a topical reasoning tree with node editing, branch generation, feedback requests, and controls for pausing and collapsing the display. Source: Pang et al. (2026), Figure 1 in the reviewed manuscript, PDF page 4; cropped from the original paper.](figures/pang2026hippo.png)

Collapsing a subtree appends a summary beneath its parent. After editing, users request a response based on the updated reasoning. Hovering over response sentences highlights associated reasoning nodes. These operations connect local text with a larger argument, but they also introduce generated structure and summaries that need to be checked against the original wording.

The implementation uses DeepSeek-R1 for the reasoning material and GPT-4o for three operators: Structure, Clarify, and Link. Structure marks topical hierarchy with XML-like tags. Clarify identifies passages that could benefit from feedback. Similarity checking suppresses repeated clarification questions. Link associates reasoning passages with response sentences through a prompted semantic-inference task.

Edited reasoning is placed inside thought delimiters and supplied with the original query to obtain an updated response. This is a concrete form of text-mediated steering. It is distinct from resuming a saved internal model state or establishing that the original trace was a faithful account of the computation that produced the first answer.

#### Study design and reported outcomes

Sixteen participants compared Hippo with an editable linear reasoning interface in a counterbalanced within-participant study. All used LLM chatbots at least weekly. The baseline allowed inline edits before revealing the response, making the comparison more informative than contrasting editable reasoning with a wholly read-only alternative.

The two tasks were daily ethical dilemmas involving a parent's financial independence and a friend's overuse of hospitality. These tasks permit contextual tradeoffs and personalization. They do not provide a simple objective answer key, which limits what the study can conclude about accuracy or appropriate reliance.

On seven-point scales, Hippo received higher ratings for control, 5.75 versus 4.19; sensemaking, 6.44 versus 5.19; and awareness of assumptions, 6.25 versus 4.69. The reported differences were statistically significant. Participants also rated the layout more favorably. These are measures of perceived experience, supplemented by observed interaction and interviews, rather than objective tests of reasoning comprehension.

Decision confidence rose from 5.06 to 6.06, with a reported p-value of 0.049. However, differences in useful insights, response satisfaction, caution, and intended future use were not statistically significant. The study therefore does not support describing Hippo as uniformly improving all measured outcomes. Increased confidence also cannot establish calibration without an independent account of when the participant's decision was warranted.

Participants described the resulting response as more personal and reported that their contributions appeared in it. Yet spontaneous edits were sparse; prompted feedback nodes played an important role in eliciting contributions. Some users appreciated this guidance, while others found repeated questions burdensome or interpreted them as a sign of model weakness. No participant collapsed the tree during its progressive presentation in the main study, and only three did so after completion.

The two follow-up cases concerned neuroscience information seeking and acquisition planning. They illustrate different preferences for detail and interruption. One user wanted to reach the final response sooner after obtaining enough information; the other used collapsing and domain-specific feedback to organize a more deliberate review. These cases broaden the design discussion without supplying controlled evidence for expert decision quality.

#### Interpretation and relationship to the collection

The paper's strongest evidence concerns perceived control and engagement with assumptions. It explicitly states that the work does not systematically analyze how feedback changes model behavior or establish more accurate outputs. The hierarchy, feedback classifier, and response links also lack a comprehensive independent accuracy evaluation in the reviewed study.

Hippo connects Sensecape's multilevel organization with the editable alternatives of iToT. Compared with ReTrace, it makes revision part of the workflow; compared with AGDebugger, it changes reasoning text rather than restoring a multi-agent execution checkpoint. Its task setting also differs from Zhou et al.'s objective mathematical verification.

For future research, Hippo suggests that an intermediate artifact can be valuable even when the final answer becomes only a summary of the user's deliberation. Testing that possibility requires separating preference alignment, factual accuracy, and critical engagement. An interface may help users express what they want while still requiring independent checks on whether the resulting recommendation is well supported.

### 30. Improving Human Verification of LLM Reasoning through Interactive Explanation Interfaces

**Reviewed source:** Zhou et al. (2026). *Improving Human Verification of LLM Reasoning through Interactive Explanation Interfaces*.

#### Problem and contribution

Zhou et al. investigate whether interactive explanation formats help people verify mathematical reasoning and locate erroneous steps. This is a narrower and more directly testable question than whether an interface feels transparent. The paper compares traditional CoT text with interactive CoT, interactive Program-of-Thought, and an interactive graph.

Its contributions are three presentation formats, a pipeline that transforms common tagged content into those formats, and a between-participant study with 125 analyzed participants. The local paper includes the IUI 2026 publication information. It also contains editorial inconsistencies, including a placeholder running author and conflicting model names in the methods and disclosure. The review uses the substantive methods description and flags those inconsistencies rather than treating every template field as authoritative.

#### Interface formats and common content

Interactive CoT divides the explanation into navigable text steps. Interactive Program-of-Thought presents code-like operations and changing variable values. The interactive graph represents variables, intermediate values, and results as nodes connected by operations. The formats share a dual-panel arrangement, a problem summary, consistent variable colors, and navigation or playback controls, with some differences in progressive display for the code-like interface.

![The study compares traditional text with interactive CoT, code-like reasoning, and a graph representation of the same mathematical explanation. Source: Zhou et al. (2026), Figure 2, PDF page 5; cropped from the original paper.](figures/zhou2026verification.png)

An intermediate representation tags facts, steps, formulas, calculations, variables, errors, and the final output. Interface templates constrain the subsequent HTML generation. The methods identify Claude 3.7 Sonnet as the generation model. This arrangement aims to preserve common reasoning content while varying its presentation, avoiding a comparison in which different interfaces happen to receive different solutions.

The controlled error information belongs to stimulus construction and scoring. It should not be interpreted as a deployed system that automatically knows which step is wrong. Likewise, generating an interface from a structured representation does not itself prove semantic equivalence; reliable use outside the prepared study would require validation of both tags and rendered behavior.

#### Participants, materials, and measures

The stimulus pool contained 500 explanations derived from GSM8K: fifty correct explanations and 450 erroneous ones, divided equally among nine error categories. The categories included calculation, counting, context values, contradictory or missing steps, hallucination, unit conversion, operators, and formula confusion. Explanations were selected to contain four to seven reasoning steps.

The experiment recruited 129 undergraduates at two U.S. universities and excluded four whose average response times fell outside the authors' screening thresholds. The remaining 125 participants had completed mathematics beyond high school. Each was randomly assigned to one format and judged ten explanations, consisting of one correct answer and one example of each of the nine error types. Participants identified correctness and, for an incorrect answer, the erroneous step. There was no per-question time limit.

The paper separately measures verification accuracy, localization of the wrong step, response time, interaction logs, and subjective experience. This separation is valuable because noticing that an answer is wrong is different from finding the point at which it becomes wrong.

#### Results and statistical boundaries

Reported verification accuracy was 73.5 percent for traditional CoT, 80.6 for interactive CoT, 82.5 for the code-like format, and 85.6 for the graph. The paper reports significant corrected comparisons between each interactive condition and the traditional baseline. Differences among the three interactive formats were not statistically significant after correction. The graph therefore had the highest observed mean, but the experiment does not establish its superiority over both interactive alternatives.

Wrong-step localization was reported as 66.1 percent for traditional CoT, 79.3 for interactive CoT, 80.1 for the code-like format, and 85.2 for the graph. These results provide more direct support for useful human checking than a preference rating alone. However, the manuscript repeats identical omnibus statistics across distinct outcomes, a reporting issue that should be resolved against the underlying analysis before relying on those exact test values.

Mean response time was 64.7 seconds for traditional CoT, 59.5 for interactive CoT, 60.1 for the code-like format, and 57.9 for the graph. None of the pairwise time differences reached the reported corrected significance threshold. The abstract's faster-time framing therefore needs the qualification that the observed differences were descriptive rather than established pairwise effects.

Subjective ratings generally favored the interactive conditions, with differences in which format appeared most engaging or desirable for future study. Because participants experienced only their assigned format, these ratings are between-group assessments rather than a direct preference ranking by people who tried all four interfaces. Feature ratings also cannot isolate the causal contribution of color, summaries, or playback without corresponding ablations.

#### Limits and relationship to the collection

The one-to-nine ratio of correct to incorrect answers creates an unusually error-heavy environment. A participant who always chose “incorrect” would achieve ninety percent on binary correctness classification, although that strategy would not solve localization. This makes the separate localization measure essential and limits the interpretation of overall verification accuracy as evidence of deployment-ready reliance calibration.

The study tests knowledgeable undergraduates on short grade-school explanations with controlled errors. It does not establish learning gains for children, performance on naturally occurring long traces, or transfer to professional domains. The appendix reports no significant format differences within individual error categories; the aggregate result should not be expanded into a claim of demonstrated improvement for every error type.

Compared with HoT, this paper finds favorable aggregate verification effects for a richer package of structure and interaction. The studies differ in stimuli, error prevalence, participants, and controls, so the results are not contradictory estimates of one identical treatment. Together they motivate experiments that hold content and error prevalence constant while separately varying highlights, source summaries, graph structure, and navigation. That would clarify which components help people reject incorrect reasoning and under what conditions.

### Synthesis of Part V

These papers span exploration, steering, personalization, and verification. Their outcomes should remain attached to those tasks. Sensecape demonstrates changes in represented coverage and organization. iToT demonstrates controllable candidate generation through cases. Hippo provides comparative evidence about perceived control and sensemaking. Zhou et al. measure correctness judgments and error localization under controlled conditions.

The shared opportunity is to let users act on a meaningful unit of information while retaining its context. The unresolved challenge is to ensure that the unit, its links, and its scores accurately represent the underlying material. A useful interface can expose a point of intervention; reliable human-AI work also requires knowing whether that intervention improved the result.


## Part VI. Human Performance, Metacognition, and Trust

The final part retains the source report's emphasis on the consequences of showing reasoning to people. These papers test trace verbosity, certainty framing, and graphical rationales. They provide a useful endpoint for the collection because they ask whether the experience of understanding corresponds to better judgment. Their findings also return to Part I's distinction between a persuasive explanation and an explanation that supports a warranted conclusion.

### 31. Explaining Too Much? Understanding How Large Language Model Reasoning Traces Influence Performance and Metacognition

**Reviewed source:** Fernandes et al. (2026). *Explaining Too Much? Understanding How Large Language Model Reasoning Traces Influence Performance and Metacognition*.

#### Problem and contribution

Fernandes et al. examine how displaying reasoning traces affects problem performance and metacognition. Metacognition concerns how people monitor and evaluate their own thinking. In this setting, a person may feel that an AI-assisted answer is well reasoned while inaccurately estimating how many problems they solved correctly.

The paper reports a preregistered, between-participant experiment with 559 analyzed participants. It compares answer-only assistance, a full trace presented before the answer, and a summary trace presented with the answer. The local file is a May 2026 arXiv preprint carrying working-draft markings and anonymized resource links. It should be cited as a preprint rather than an established ACM proceedings publication.

The contribution is the joint measurement of objective performance, global performance estimates, trial-level confidence, trust, workload, and user experience. This allows the authors to examine whether a favorable interface experience corresponds to better reasoning or more accurate self-evaluation.

#### Conditions and methodological controls

Participants solved ten LSAT-style logical reasoning problems. The answer-only and summary conditions used GPT-5. The full-trace condition used gpt-oss-20b because it exposed the intermediate text required for that presentation. The retained items were screened so that both models answered five of the ten correctly. Matching aggregate answer performance reduces one difference between models, but it does not equate their wording, error mechanisms, conversational behavior, or rationale quality.

The full trace appeared before a button allowed the participant to reveal the final answer. The summary condition displayed summary and answer together. Thus, model identity and answer-reveal behavior both vary with the full-trace treatment. The cleanest contrast is between answer-only and summary assistance, where the model is held constant. The experiment cannot isolate verbosity alone across all three conditions.

![The Full-trace condition displays the reasoning before a button reveals the final answer; the study also compares answer-only and summary-with-answer conditions. Source: Fernandes et al. (2026), Figure 2, PDF page 8; cropped from the original preprint.](figures/fernandes2026explaining.png)

Participants had to interact with the model at least once per problem and could continue through unrestricted free-text exchanges. They then selected an answer and rated confidence. At the end, they estimated their total correct answers. The study also collected standard questionnaires and open-ended descriptions of how the AI was used.

The sample came from U.S.-based, English-fluent Prolific participants. Group sizes were 187 for answer-only, 183 for full traces, and 189 for summaries. This is a substantially larger participant sample than most prototype studies in the collection, although the ten-item task battery still limits the precision of individual metacognitive measures.

#### Performance and calibration results

Mean achieved scores were 6.18 out of ten for answer-only, 5.46 for full traces, and 6.11 for summaries. The full-trace condition performed significantly worse than both alternatives. Answer-only and summary scores did not differ significantly. This supports the conclusion that summaries did not produce a detected performance benefit in the controlled same-model comparison; it is not a formal equivalence test establishing identical performance.

All three group means exceeded the screened model-alone score of five, with significant comparisons reported in the results. A later discussion passage characterizes full-trace performance as sitting at the model benchmark, which overstates the similarity. The numerical results support a smaller gain over that benchmark, not no gain. There was also no unaided-human condition, so the experiment does not directly estimate improvement over people solving the same items without AI.

Participants estimated approximately eight correct answers in every condition. Their mean overestimation was 1.74 items for answer-only, 2.44 for full traces, and 1.96 for summaries. Full-trace overestimation was significantly greater than answer-only overestimation. The summary condition did not differ significantly from either alternative on that measure.

Trial-level analyses distinguish sensitivity from calibration. Participants generally assigned somewhat higher confidence to correct than incorrect responses, but the confidence gap and type-two AUROC did not differ significantly among conditions. Full traces produced greater absolute overconfidence and worse Brier scores. These findings should not be collapsed into a claim that every aspect of metacognitive sensitivity deteriorated; the strongest differences concern calibration and combined forecast quality.

Trust and hedonic appeal increased in both trace conditions relative to answer-only. Overall workload and System Usability Scale scores did not differ significantly. A reader might therefore experience the trace as more appealing and trustworthy without noticing an increase in workload or recognizing the accompanying performance limitation.

#### Interpretation and relationship to the collection

A mediation analysis found an indirect association between trace condition and overestimation through hedonic appeal after accounting for trust. The authors interpret this as consistent with a processing-fluency account: an appealing interaction may be mistaken for evidence of competent joint reasoning. Because the mediators were measured rather than independently manipulated, the analysis does not establish that mechanism causally or rule out alternative explanations.

Qualitative responses described offloading, guided reasoning, comparison with an independently formed answer, and burdensome verbosity. These accounts suggest different uses of the same interface. They do not independently establish that a reported comparison strategy produced calibrated decisions. The proposed intervention of eliciting a user's own reasoning before showing AI output is a future design direction, not a treatment validated by this experiment.

This paper complements Hippo's positive ratings of control by showing why subjective measures need behavioral counterparts. It also strengthens the case for evaluating summaries as transformations with specific effects, rather than assuming that either more detail or less detail is always better. Its conclusion is bounded but important: under the tested conditions, trace exposure improved aspects of experience without improving objective performance or self-evaluation, and the full-trace package produced worse outcomes than the alternatives.

### 32. Seeing the Reasoning: How LLM Rationales Influence User Trust and Decision-Making in Factual Verification Tasks

**Reviewed source:** Sun et al. (2026). *Seeing the Reasoning: How LLM Rationales Influence User Trust and Decision-Making in Factual Verification Tasks*.

#### Problem and contribution

Sun et al. treat a reasoning rationale as an interface element whose presentation and language can influence reliance. The paper asks how three properties affect users: when the rationale is revealed, whether its reasoning is correct, and how certain it sounds. The contribution is a controlled online study of these factors, supported by qualitative responses about desired explanation features.

The work appears in the CHI 2026 Extended Abstracts. The local file is a June 2026 arXiv revision of that short paper. Its scope is factual-verification interaction with prepared responses. It does not evaluate an open-ended conversational assistant that independently retrieves evidence or adapts its uncertainty estimates during use.

The distinction between rationale correctness and answer correctness is especially important here. The experiment changes the rationale while retaining the associated answer. An incorrect rationale can therefore accompany a correct answer, as the paper's Miami example illustrates. Reduced acceptance of an answer after seeing a flawed rationale is a change in reliance, but it is not automatically an improvement in answer accuracy.

#### Experimental design and interface

Sixty-eight English-speaking Prolific participants completed a mixed-design experiment. Presentation format varied between participants: instant, delayed, or on demand. Rationale correctness and certainty framing varied within participants. Each person completed six trials covering correct and incorrect rationales crossed with no certainty cue, a certain cue, and an uncertain cue.

In the instant condition, rationale and answer appeared together. In the delayed condition, the rationale appeared after a brief delay proportional to its length. In the on-demand condition, it was initially hidden behind a show/hide control. These are relatively lightweight presentation changes; the experiment does not test the richer multilevel navigation used by Sensecape or ReTrace.

![The study interface presents a query, an answer, a rationale, an optional certainty statement, and a show/hide control in the on-demand condition. Source: Sun et al. (2026), Figure 1, PDF page 2; original interface panel reproduced from the paper.](figures/sun2026seeing.png)

The certainty manipulation appends a short statement expressing confidence or hesitation about the reasoning. It is a surface-language cue, not a calibrated probability derived from model uncertainty. Holding the substantive rationale fixed while changing that cue allows the study to examine persuasion through framing.

The prepared stimuli use short factual claims and comparable rationale length and structure. Incorrect rationales contain a controlled factual or logical flaw. Participants decide whether to accept the answer and report decision confidence, trust in the information, and trust in the LLM system. They also complete a manipulation check and provide open-ended comments. The sample was highly educated, with all participants reporting at least a bachelor's degree, which bounds generalization to less educated or less familiar populations.

#### Findings and what they establish

The reported main effects favor correct rationales over flawed ones for trust, confidence, and advice adoption. Descriptively, answer adoption was 0.94 with correct rationales and 0.86 with incorrect rationales. Trust in the information averaged 4.09 versus 3.81 on a five-point scale. These results indicate that participants responded to the quality of the displayed reasoning rather than ignoring it entirely.

Certainty framing also shifted responses. Adoption averaged 0.96 with certain language, 0.91 without a cue, and 0.84 with uncertain language. Decision-confidence means were 5.96, 5.59, and 5.31, respectively, on a seven-point scale. The paper reports significant effects and post-hoc differences for several trust and decision measures. The practical concern is that wording can move reliance even when the underlying evidence has not changed.

Presentation format did not produce a significant detected effect. That result is limited to the three implementations, six-trial exposure, and available sample. It does not establish that reveal timing or on-demand controls never matter. In particular, richer controls for requesting evidence or selecting explanation depth were not part of the manipulation.

Participants described checking individual reasoning steps, looking for omitted context, and reacting negatively to contradictions between an answer and its rationale. They requested stepwise explanations, links to supporting evidence, summaries with expandable detail, uncertainty information, and opportunities for follow-up. These are useful design requirements derived from reported experience, not implemented features whose effectiveness was tested in this study.

#### Limits and relationship to the collection

The study demonstrates shifts in trust and adoption more directly than it demonstrates calibrated reliance. Calibration requires relating reliance to a suitable correctness criterion and considering both warranted acceptance and warranted rejection. Because rationale quality and answer validity are not independently crossed, the experiment cannot fully separate skepticism toward bad reasoning from successful rejection of a wrong answer.

A discussion passage compares incorrect rationales with showing no rationale, although the design includes a no-certainty-cue condition rather than a separate no-rationale baseline. That particular comparison is unsupported by the stated experimental conditions. The review therefore restricts the conclusion to observed differences in rationale quality, framing, and reveal format.

Sun et al. complement Kuhn et al. by showing why the presentation of uncertainty needs its own evaluation. A score that predicts error and a sentence that sounds uncertain are different objects. They also complement HoT: visual linkage and confident wording can both change user behavior without improving the underlying answer. The resulting research requirement is to couple certainty communication with evidence about reliability and to evaluate the cost of both excessive acceptance and excessive rejection.

### 33. Graphionale: How Graph Visualizations of LLM Rationales Affect Human Decision Making

**Reviewed source:** Wang et al. (2026). *Graphionale: How Graph Visualizations of LLM Rationales Affect Human Decision Making*.

#### Problem and contribution

Wang et al. examine when argument-map representations help users evaluate LLM rationales. Graphionale combines a co-design study, a prototype that generates structured graphs with compressed node contents, a technical evaluation, and a 204-participant experiment. Its central finding is that the effect of graphical presentation reverses between the tested verbal and visual reasoning tasks.

The local manuscript was posted in August 2026 and carries publication information for UIST in November 2026. As of this whitepaper's September 8, 2026 cutoff, that conference is forthcoming. The review includes the available manuscript and distinguishes its current availability from the future event date.

Graphionale is an argument-map interface, not a visualization of model activations. It also uses answer-conditioned rationales, including rationales generated for selected incorrect answers. The study therefore concerns how people respond to displayed justifications rather than whether those justifications faithfully reveal the computation of an independently produced answer.

#### Design and technical evaluation

Ten daily LLM users participated in formative co-design. They identified the need to compress text, align the layout with comparison and elimination, clarify the meaning of edges, and bound graph complexity through progressive disclosure. These requirements informed a two-stage procedure: construct an argument map and compress statements within its nodes.

The map contains premises, intermediate conclusions, and a final conclusion, with support and objection relationships. Node contents become short labels or entity-relation-entity representations. Users can reveal full text on hover and expand or collapse supporting and opposing branches. The evaluated interface is read-only with respect to rationale content; editing reasoning and regenerating from it is future work.

![Graphionale combines an argument graph with compressed node contents, support and objection branches, progressive disclosure, and access to full statements. Source: Wang et al. (2026), Figure 1, PDF page 1; cropped from the original manuscript.](figures/wang2026graphionale.png)

The implementation generates a common argument map and derives both graphical and organized textual rationales from it. This makes the baseline more demanding than unstructured prose and helps hold content constant. The pipeline still depends on the correctness of generated structure and compression.

Two coders examined 180 rationales across six task categories after iterative prompt refinement. Five structural issues were reported. Among 120 correct-answer rationales, fifteen contained redundant reasoning and ten included visual claims that were difficult to verify. Incorrect-answer rationales exhibited missing evidence, problematic evidence, and faulty conclusions, with categories that could overlap. High structural compliance should therefore not be read as equivalent to semantic correctness. The refinement process also means these results describe the finalized prompt on the evaluated materials, rather than a wholly untouched test of generalization.

#### Controlled study and measures

The main study crossed text versus graph with verbal versus visual reasoning between participants. Verbal tasks came from BIG-Bench Hard; visual tasks came from I-RAVEN. Difficulty varied within participants. Of 223 recruited participants, 204 passed the attention checks.

Each participant completed fifteen trials, including five easy and ten hard questions. Five trials were associated with an incorrect-answer rationale. Participants first gave an initial answer, then reviewed the rationale, and finally revised their decision. The display omitted a separate explicit answer recommendation, although the rationale could still convey its conclusion.

The paper operationalizes appropriate trust, over-trust, under-trust, and error correction through participants' final decisions relative to the rationale's associated answer. Error correction requires choosing the correct alternative, making it stricter than merely rejecting the AI's position. These are behavioral reliance measures, distinct from the separately collected trust ratings.

#### Results and interpretation

For verbal reasoning, graphical rationales reduced over-trust by an estimated 14.4 percentage points and increased error correction by 12.7 points when collapsed across difficulty. The benefits were concentrated in hard questions in the stratified analysis. The broader appropriate-trust measure showed a weaker pattern, so the result should be described through the particular measures that improved rather than as an undifferentiated gain in all aspects of trust.

For visual reasoning, the graph reduced appropriate trust by 16.5 percentage points, increased under-trust by 18.6 points, and reduced error correction by 23.3 points. These effects occurred across the tested difficulty levels. They concern this argument-map representation of visual tasks, not all possible graphical explanations. Source-image overlays or attribute-linked annotations might behave differently.

Subjective experience ran in the opposite direction. In verbal reasoning, graphs received lower usability and satisfaction ratings and higher workload ratings despite favorable behavioral results on over-trust and correction. In visual reasoning, graphs were rated more satisfying, engaging, and helpful despite worse calibration measures. Visual-task participants also spent less time with graphs, 28.2 versus 36.7 seconds per trial. Faster processing therefore did not imply better verification.

The authors propose a mismatch between abstract argument structure and the perceptual demands of I-RAVEN. Participant requests for source-image highlights support that interpretation, but the study does not independently manipulate perceptual grounding to establish the mechanism. Exploratory analyses of need for cognition suggest further differences in how users engage; median-split patterns should remain exploratory rather than becoming a rule for assigning interfaces to individuals.

#### Relationship to the collection

Graphionale provides one of the clearest demonstrations that interface preference and behavioral benefit can diverge. It qualifies any broad claim that converting prose into a graph improves human reasoning. Its comparison also helps explain why positive results from short mathematical explanations cannot be generalized to every visual task.

The paper connects ReasonDiag's argument dependencies, ReTrace's progressive disclosure, and Fernandes et al.'s metacognitive concerns. It leaves open how editable graphs, grounded visual annotations, and repeated real-world use change the outcome. Its strongest contribution is a conditional account: representation matters through its relationship to the task and the user, and successful design must be judged by warranted decisions as well as satisfaction.

### Synthesis of Part VI

The three studies examine different interventions, but each separates some aspect of experience from the quality of judgment. Fernandes et al. find improved trust and appeal without a detected performance benefit from summaries. Sun et al. show that certainty language changes adoption independently of the substantive rationale. Graphionale demonstrates opposite behavioral effects across task modalities alongside preference patterns that favor the less effective format in each setting.

These findings do not justify withholding all explanations or preferring one universal format. They support a more precise research program: identify the decision a user must make, preserve access to its evidence, and evaluate whether the interface helps the user accept sound reasoning, reject flawed reasoning, and recognize the limits of their own judgment.


## Cross-Paper Synthesis and Research Directions

### From visible information to accountable decisions

The six-part organization supports a progression from explanation validity to human consequences. Its value is not that every paper contributes to a single technical pipeline. The papers study different objects and establish different kinds of evidence. Their combined contribution is a set of requirements for connecting an explanation, an interface, and a human decision without assuming that success at one level guarantees success at another.

A useful starting point is the question a person needs to answer. A model researcher may ask which activation contributes to a token prediction. A workflow author may ask which intermediate output caused a downstream failure. A reader may ask whether a stated premise is supported by the source. A decision maker may ask whether to accept an answer. These questions require different evidence, even when the interface presents each as a graph or highlighted sequence.

Turpin et al. (2023), Lanham et al. (2023), and Jacovi and Goldberg (2020) constrain the claims that can be made about reasoning text. LM-Debugger, the Tuned Lens, and Patchscopes provide ways to investigate model representations, but their decoded tokens and intervention results do not automatically validate a separate written rationale (Geva et al., 2022; Belrose et al., 2023; Ghandeharioun et al., 2024). Conversely, a rationale can help a person solve or check a problem without being a complete account of the model's computation. The review therefore treats computational faithfulness and human usefulness as separate evaluation targets.

### Representation, interaction, and evidence

The following comparison groups systems by the information they expose. It is a design map derived from the reviewed papers, rather than an additional classification of the corpus. Papers retain their original placement in the six parts.

| Representation and examples | Main human operation | Evidence available | Remaining question |
|---|---|---|---|
| Attention and embedding views: BertViz, exBERT, AttentionViz | Select, compare, filter, and retrieve patterns | Computed model quantities and corpus examples | Does the pattern explain an output or support a successful diagnosis? |
| Decoded or modified activations: LM-Debugger, Tuned Lens, Patchscopes | Inspect a decoding or intervene in a representation | Controlled changes and decoding experiments | What depends on the decoder, target prompt, or intervention choice? |
| Workflow and execution views: AI Chains, PromptChainer, AGDebugger, WaitGPT | Edit a unit, inspect state, and rerun | Intermediate artifacts, messages, operations, and observed outputs | Does a local change repair the task without causing downstream failures? |
| Comparison views: ChainForge, LLM Comparator | Vary inputs, models, prompts, or criteria | Sampled outputs and evaluator judgments | Are the test cases representative and the evaluators reliable? |
| Reasoning and argument views: ReasonGraph, ReasonDiag, ReTrace, Graphionale | Follow branches, dependencies, phases, or supporting claims | Parsed or model-derived structure tied to explicit text | Is the structure accurate, and does it support the intended judgment? |
| Authoring and exploration views: SPROUT, Sensecape, iToT, Hippo, CoAuthor | Generate, select, revise, organize, or provide feedback | Alternatives, revisions, interaction records, and reported experience | Do useful edits and broader exploration improve final outcomes? |
| Reference and verification views: HoT and Zhou et al. | Match facts, step through a solution, and identify an error | Visible source references and structured intermediate steps | Does easier reading improve both acceptance of correct work and rejection of incorrect work? |

The table reveals a recurring design pattern: an overview supports a local inspection, and the local inspection can lead to a judgment or action. The overview may be an embedding plot, a workflow graph, a phase layout, or an argument map. Its value depends on what becomes available when a person selects an element. Access to the corresponding source text, execution state, or original input gives the representation something concrete to explain.

The papers also expose a recurring failure opportunity. A derived graph can contain an incorrect dependency; a summary can omit a qualification; a highlighted span can create an impression of support without checking whether the cited fact entails the claim. ReasonDiag's precision results and SPROUT's linkage errors make this problem measurable. Graphionale's technical inspection and modality-dependent behavioral results show why a technically plausible representation also needs a human evaluation (Chen et al., 2026; Liu et al., 2025; Wang et al., 2026).

### Control should be evaluated through its consequences

Several systems give users a concrete unit of control, but the scope of that control differs. Changing a PromptChainer node changes a workflow operation. Editing a WaitGPT operation changes supported analysis code. Resetting AGDebugger at a checkpoint modifies subsequent agent execution under the system's reset procedure. Editing Hippo's explicit thought text changes material used in further generation; it does not expose an arbitrary model-state editor. Selecting an iToT branch chooses among generated alternatives. These operations should be compared through their actual semantics, rather than grouped under a general claim of controlling internal reasoning.

The human studies provide useful evidence about usability and perceived agency. AI Chains supports greater reported control, SPROUT improves several authoring ratings, and Hippo improves reported control and awareness of assumptions. AGDebugger also demonstrates why these measures need an outcome companion: participants can make many plausible edits while few runs reach the exact correct answer (Wu, Terry, and Cai, 2022; Liu et al., 2025; Pang et al., 2026; Epperson et al., 2025).

A future intervention study could measure a sequence of outcomes: whether the user locates the relevant problem, whether the selected edit addresses it, whether the rerun repairs it, and whether unrelated requirements remain satisfied. This would distinguish an interface that makes intervention comfortable from one that helps users intervene effectively. Recording the original state, edited artifact, rerun configuration, and resulting output would make failures interpretable and allow comparison with observational records such as CoAuthor.

### Scores need an explicit interpretation

The collection contains several numerical signals that can look like confidence when displayed in an interface. Attention weights describe an attention operation. Semantic entropy measures dispersion across meaning clusters under a sampling and equivalence procedure. A process reward score reflects a trained assessment of steps. A tree-search evaluation ranks candidate thoughts under a model's criterion. An LLM judge provides a comparative judgment. These signals do not share one probability interpretation.

Kuhn et al. (2023) evaluate uncertainty through discrimination between correct and incorrect answers, not a universal guarantee that a displayed value equals a calibrated error probability. Lightman et al. (2024) and Wang et al. (2024) improve mathematical solution selection under specific candidate budgets and verifier procedures. Boyle et al. (2024) show a case in which a person needs to override the model's preferred thought. Each result supports displaying the signal's source and meaning, along with the evidence required to challenge it.

A verification interface could therefore distinguish three separate fields: the generated claim, the evidence or test associated with it, and the result of that test. The proposal follows from the review; it is not an implemented feature common to these papers. Its evaluation would ask whether users understand what a score measures and can recognize cases in which the score is confidently wrong.

### Human benefit is conditional on task and study design

The controlled studies do not support a universal ordering of text, summary, highlight, and graph formats. ReTrace supports some interpretation tasks and reduces perceived effort, but its correctness task has a ceiling and its time results do not establish a general speed benefit. Zhou et al. report higher aggregate verification and localization with interactive formats, but their trial distribution is heavily weighted toward incorrect solutions. HoT reduces judgment time while reducing rejection of incorrect answers. These findings concern different tasks and baselines and should not be combined into a pooled performance estimate (Felder et al., 2026; Zhou et al., 2026; Nguyen et al., 2026).

Part VI adds three further constraints. Fernandes et al. (2026) vary both presentation and aspects of model and answer-reveal behavior, so the full-trace condition estimates the effect of that experimental package. Sun et al. (2026) find effects of certainty wording, while their presentation-timing comparison does not establish the advantage claimed in the supplied synthesis report. Graphionale finds behavioral benefits on particular verbal-reasoning measures and harms on visual reasoning, with subjective experience moving in the opposite direction (Wang et al., 2026).

Together, these results make separate acceptance and rejection measures essential. Overall accuracy can conceal a shift toward accepting everything, especially when correct answers are common. It can also conceal a shift toward rejecting everything when incorrect examples dominate. Error localization and successful correction provide additional evidence because they require a user to identify or repair the problem, rather than merely choose a binary response.

### A focused research agenda

The following questions translate the collection's unresolved issues into studies. They are proposals based on this review, not findings attributed to the source papers.

| Research question | Concrete comparison | Primary outcome and necessary control |
|---|---|---|
| Does access to original evidence improve verification? | A derived graph with source links versus the same graph without links | Correct acceptance and rejection; identical rationale content and balanced correctness conditions |
| Does accurate structure matter independently of visual format? | Text and graph crossed with validated and deliberately perturbed dependencies | Error localization and correction; separately inspect conversion fidelity |
| Which intervention unit supports successful repair? | Editing a step, premise, or workflow node on matched failures | Final task correctness and collateral errors; fixed model, rerun budget, and starting failure |
| Can calibrated score displays improve reliance? | A defined, validated score versus an unqualified confidence label | Reliance conditioned on correctness and calibration of users' judgments; include confidently wrong cases |
| Does perceptual grounding explain the visual-task deficit? | Argument maps with and without links to source-image attributes | Appropriate reliance and visual error localization; hold argument text and layout constant |
| Do interface effects persist after repeated use? | Repeated sessions with stable interfaces and changing task instances | Learning, verification effort, and error sensitivity over time; measure prior expertise and order effects |

The first two questions connect Parts I, II, and IV. They ask whether the structure is valid and whether access to evidence changes human judgment. The third connects workflow debugging with interactive reasoning. The fourth joins uncertainty and verifier research with the behavioral concerns in Part VI. The fifth directly tests the perceptual-grounding explanation proposed for Graphionale's results. The sixth addresses the short sessions and constrained tasks common across the collection.

For an initial study, the clearest contribution would come from isolating one mechanism. A source-linked argument map offers a tractable example. The study could hold rationale wording constant, validate the map against the original text, and vary whether users can inspect supporting input evidence from each claim. Participants would first answer independently, then inspect assistance and revise their judgment. Correct and incorrect rationales would be analyzed separately, with localization and confidence collected alongside the final answer. This would test whether the interface supports warranted revision rather than merely increasing agreement with the model.

Such a study should report time and experience measures as secondary outcomes with their own interpretation. A slower format may support better checking; a preferred format may encourage premature acceptance. Content conversion errors, failed interactions, and unsuccessful interventions should remain visible in the analysis. The reviewed literature provides enough evidence to make these possibilities central research questions rather than incidental limitations.

### What the collection establishes

The thirty-three papers establish a broad set of methods for inspecting representations, exposing intermediate artifacts, authoring workflows, visualizing explicit reasoning, and studying human response. They also show that the meaning of an explanation depends on its construction and use. A readable rationale can omit an influential cause. A useful graph can encode an inaccurate relation. A reassuring interface can increase trust without improving judgment. An intervention can feel effective without repairing the answer.

The strongest research direction supported by the collection connects a specific representation to a specific human operation and evaluates the resulting decision. That approach preserves the source report's progression from reasoning faithfulness to human evaluation while making the evidential link between those parts explicit.


## References

All authors are listed. Publication metadata identifies the cited work; Appendix A identifies the local version reviewed. DOI links and repository records were checked against available records on September 8, 2026.

Ian Arawjo; Chelse Swoopes; Priyan Vaithilingam; Martin Wattenberg; Elena L. Glassman. (2024). **ChainForge: A Visual Toolkit for Prompt Engineering and LLM Hypothesis Testing.** *Proceedings of the CHI Conference on Human Factors in Computing Systems, pp. 1–18. ACM*. [DOI: 10.1145/3613904.3642016](https://doi.org/10.1145/3613904.3642016); [arXiv:2309.09128](https://arxiv.org/abs/2309.09128).

Nora Belrose; Igor Ostrovsky; Lev McKinney; Zach Furman; Logan Smith; Danny Halawi; Stella Biderman; Jacob Steinhardt. (2023). **Eliciting Latent Predictions from Transformers with the Tuned Lens.** *arXiv preprint*. [DOI: 10.48550/arXiv.2303.08112](https://doi.org/10.48550/arXiv.2303.08112); [arXiv:2303.08112](https://arxiv.org/abs/2303.08112). Preprint; reviewed arXiv 2303.08112v6.

Alan Boyle; Isha Gupta; Sebastian Hönig; Lukas Mautner; Kenza Amara; Furui Cheng; Mennatallah El-Assady. (2024). **iToT: An Interactive System for Customized Tree-of-Thought Generation.** *IEEE VIS 2024 NLVIZ Workshop: Exploring Research Opportunities for Natural Language, Text, and Data Visualization*. [Publication record](https://arxiv.org/abs/2409.00413); [arXiv:2409.00413](https://arxiv.org/abs/2409.00413). Workshop paper; local manuscript 8 pages; no separate proceedings pagination verified.

Shiwei Chen; Niruthikka Sritharan; Xiaolin Wen; Chenxi Zhang; Xingbo Wang; Yong Wang. (2026). **When the Chain Breaks: Interactive Diagnosis of LLM Chain-of-Thought Reasoning Errors.** *Computer Graphics Forum, 45(3), Article e70439. Wiley*. [DOI: 10.1111/cgf.70439](https://doi.org/10.1111/cgf.70439); [arXiv:2603.21286](https://arxiv.org/abs/2603.21286).

Will Epperson; Gagan Bansal; Victor Dibia; Adam Fourney; Jack Gerrits; Erkang Zhu; Saleema Amershi. (2025). **Interactive Debugging and Steering of Multi-Agent AI Systems.** *Proceedings of the 2025 CHI Conference on Human Factors in Computing Systems, pp. 1–15. ACM*. [DOI: 10.1145/3706598.3713581](https://doi.org/10.1145/3706598.3713581).

Ludwig Felder; Jacob Miller; Markus Wallinger; Stephen G. Kobourov; Chunyang Chen. (2026). **ReTrace: Interactive Visualizations for Reasoning Traces of Large Reasoning Models.** *Computer Graphics Forum, 45(3), Article e70452. Wiley*. [DOI: 10.1111/cgf.70452](https://doi.org/10.1111/cgf.70452); [arXiv:2511.11187](https://arxiv.org/abs/2511.11187).

Daniela Fernandes; Daniel Buschek; Lev Tankelevitch; Thomas Kosch; Robin Welsch. (2026). **Explaining Too Much? Understanding How Large Language Model Reasoning Traces Influence Performance and Metacognition.** *arXiv preprint*. [DOI: 10.48550/arXiv.2605.25856](https://doi.org/10.48550/arXiv.2605.25856); [arXiv:2605.25856](https://arxiv.org/abs/2605.25856). Preprint; reviewed arXiv 2605.25856v1.

Mor Geva; Avi Caciularu; Guy Dar; Paul Roit; Shoval Sadde; Micah Shlain; Bar Tamir; Yoav Goldberg. (2022). **LM-Debugger: An Interactive Tool for Inspection and Intervention in Transformer-Based Language Models.** *Proceedings of the 2022 Conference on Empirical Methods in Natural Language Processing: System Demonstrations, pp. 12–21. Association for Computational Linguistics*. [DOI: 10.18653/v1/2022.emnlp-demos.2](https://doi.org/10.18653/v1/2022.emnlp-demos.2).

Asma Ghandeharioun; Avi Caciularu; Adam Pearce; Lucas Dixon; Mor Geva. (2024). **Patchscopes: A Unifying Framework for Inspecting Hidden Representations of Language Models.** *Proceedings of the 41st International Conference on Machine Learning, Proceedings of Machine Learning Research, 235, pp. 15466–15490. PMLR*. [Publication record](https://proceedings.mlr.press/v235/ghandeharioun24a.html); [arXiv:2401.06102](https://arxiv.org/abs/2401.06102).

Benjamin Hoover; Hendrik Strobelt; Sebastian Gehrmann. (2020). **exBERT: A Visual Analysis Tool to Explore Learned Representations in Transformer Models.** *Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics: System Demonstrations, pp. 187–196. Association for Computational Linguistics*. [DOI: 10.18653/v1/2020.acl-demos.22](https://doi.org/10.18653/v1/2020.acl-demos.22); [arXiv:1910.05276](https://arxiv.org/abs/1910.05276).

Alon Jacovi; Yoav Goldberg. (2020). **Towards Faithfully Interpretable NLP Systems: How Should We Define and Evaluate Faithfulness?.** *Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, pp. 4198–4205. Association for Computational Linguistics*. [DOI: 10.18653/v1/2020.acl-main.386](https://doi.org/10.18653/v1/2020.acl-main.386).

Minsuk Kahng; Ian Tenney; Mahima Pushkarna; Michael Xieyang Liu; James Wexler; Emily Reif; Krystal Kallarackal; Minsuk Chang; Michael Terry; Lucas Dixon. (2024). **LLM Comparator: Visual Analytics for Side-by-Side Evaluation of Large Language Models.** *Extended Abstracts of the CHI Conference on Human Factors in Computing Systems, pp. 1–7. ACM*. [DOI: 10.1145/3613905.3650755](https://doi.org/10.1145/3613905.3650755); [arXiv:2402.10524](https://arxiv.org/abs/2402.10524).

Lorenz Kuhn; Yarin Gal; Sebastian Farquhar. (2023). **Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation.** *The Eleventh International Conference on Learning Representations*. [Publication record](https://arxiv.org/abs/2302.09664); [arXiv:2302.09664](https://arxiv.org/abs/2302.09664).

Tamera Lanham; Anna Chen; Ansh Radhakrishnan; Benoit Steiner; Carson Denison; Danny Hernandez; Dustin Li; Esin Durmus; Evan Hubinger; Jackson Kernion; Kamilė Lukošiūtė; Karina Nguyen; Newton Cheng; Nicholas Joseph; Nicholas Schiefer; Oliver Rausch; Robin Larson; Sam McCandlish; Sandipan Kundu; Saurav Kadavath; Shannon Yang; Thomas Henighan; Timothy Maxwell; Timothy Telleen-Lawton; Tristan Hume; Zac Hatfield-Dodds; Jared Kaplan; Jan Brauner; Samuel R. Bowman; Ethan Perez. (2023). **Measuring Faithfulness in Chain-of-Thought Reasoning.** *arXiv preprint*. [DOI: 10.48550/arXiv.2307.13702](https://doi.org/10.48550/arXiv.2307.13702); [arXiv:2307.13702](https://arxiv.org/abs/2307.13702). Preprint; reviewed arXiv 2307.13702v1.

Mina Lee; Percy Liang; Qian Yang. (2022). **CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities.** *CHI Conference on Human Factors in Computing Systems, pp. 1–19. ACM*. [DOI: 10.1145/3491102.3502030](https://doi.org/10.1145/3491102.3502030); [arXiv:2201.06796](https://arxiv.org/abs/2201.06796).

Zongqian Li; Ehsan Shareghi; Nigel Collier. (2025). **ReasonGraph: Visualization of Reasoning Methods and Extended Inference Paths.** *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 3: System Demonstrations), pp. 140–147. Association for Computational Linguistics*. [DOI: 10.18653/v1/2025.acl-demo.14](https://doi.org/10.18653/v1/2025.acl-demo.14); [arXiv:2503.03979](https://arxiv.org/abs/2503.03979).

Hunter Lightman; Vineet Kosaraju; Yuri Burda; Harrison Edwards; Bowen Baker; Teddy Lee; Jan Leike; John Schulman; Ilya Sutskever; Karl Cobbe. (2024). **Let's Verify Step by Step.** *The Twelfth International Conference on Learning Representations*. [Publication record](https://openreview.net/forum?id=v8L0pN6EOi); [arXiv:2305.20050](https://arxiv.org/abs/2305.20050).

Yihan Liu; Zhen Wen; Luoxuan Weng; Ollie Woodman; Yi Yang; Wei Chen. (2025). **SPROUT: An Interactive Authoring Tool for Generating Programming Tutorials With the Visualization of Large Language Models.** *IEEE Transactions on Visualization and Computer Graphics, 31(9), pp. 4761–4775. Institute of Electrical and Electronics Engineers (IEEE)*. [DOI: 10.1109/TVCG.2024.3410523](https://doi.org/10.1109/TVCG.2024.3410523); [arXiv:2312.01801](https://arxiv.org/abs/2312.01801).

Tin Nguyen; Logan Bolton; Mohammad Reza Taesiri; Trung Bui; Anh Totti Nguyen. (2026). **HoT: Highlighted Chain of Thought for Referencing Supporting Facts from Inputs.** *Transactions on Machine Learning Research*. [Publication record](https://openreview.net/forum?id=abm6pDTbT1); [arXiv:2503.02003](https://arxiv.org/abs/2503.02003). Published June 2026; reviewed arXiv version 6, June 27, 2026.

Rock Yuren Pang; K. J. Kevin Feng; Shangbin Feng; Chu Li; Weijia Shi; Yulia Tsvetkov; Jeffrey Heer; Katharina Reinecke. (2026). **Interactive Reasoning: Visualizing and Controlling Chain-of-Thought Reasoning in Large Language Models.** *Proceedings of the 31st International Conference on Intelligent User Interfaces, pp. 852–867. ACM*. [DOI: 10.1145/3742413.3789091](https://doi.org/10.1145/3742413.3789091); [arXiv:2506.23678](https://arxiv.org/abs/2506.23678).

Ansh Radhakrishnan; Karina Nguyen; Anna Chen; Carol Chen; Carson Denison; Danny Hernandez; Esin Durmus; Evan Hubinger; Jackson Kernion; Kamilė Lukošiūtė; Newton Cheng; Nicholas Joseph; Nicholas Schiefer; Oliver Rausch; Sam McCandlish; Sheer El Showk; Tamera Lanham; Tim Maxwell; Venkatesa Chandrasekaran; Zac Hatfield-Dodds; Jared Kaplan; Jan Brauner; Samuel R. Bowman; Ethan Perez. (2023). **Question Decomposition Improves the Faithfulness of Model-Generated Reasoning.** *arXiv preprint*. [DOI: 10.48550/arXiv.2307.11768](https://doi.org/10.48550/arXiv.2307.11768); [arXiv:2307.11768](https://arxiv.org/abs/2307.11768). Preprint; reviewed arXiv 2307.11768v2.

Sangho Suh; Bryan Min; Srishti Palani; Haijun Xia. (2023). **Sensecape: Enabling Multilevel Exploration and Sensemaking with Large Language Models.** *Proceedings of the 36th Annual ACM Symposium on User Interface Software and Technology, pp. 1–18. ACM*. [DOI: 10.1145/3586183.3606756](https://doi.org/10.1145/3586183.3606756); [arXiv:2305.11483](https://arxiv.org/abs/2305.11483).

Xin Sun; Shu Wei; Jos A. Bosch; Isao Echizen; Saku Sugawara; Abdallah El Ali. (2026). **Seeing the Reasoning: How LLM Rationales Influence User Trust and Decision-Making in Factual Verification Tasks.** *Proceedings of the Extended Abstracts of the 2026 CHI Conference on Human Factors in Computing Systems, pp. 1–7. ACM*. [DOI: 10.1145/3772363.3798613](https://doi.org/10.1145/3772363.3798613); [arXiv:2603.07306](https://arxiv.org/abs/2603.07306).

Miles Turpin; Julian Michael; Ethan Perez; Samuel R. Bowman. (2023). **Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting.** *Advances in Neural Information Processing Systems, 36, pp. 74952–74965. Curran Associates, Inc.*. [DOI: 10.52202/075280-3275](https://doi.org/10.52202/075280-3275); [arXiv:2305.04388](https://arxiv.org/abs/2305.04388).

Jesse Vig. (2019). **A Multiscale Visualization of Attention in the Transformer Model.** *Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics: System Demonstrations, pp. 37–42. Association for Computational Linguistics*. [DOI: 10.18653/v1/P19-3007](https://doi.org/10.18653/v1/P19-3007).

Peiyi Wang; Lei Li; Zhihong Shao; Runxin Xu; Damai Dai; Yifei Li; Deli Chen; Yu Wu; Zhifang Sui. (2024). **Math-Shepherd: Verify and Reinforce LLMs Step-by-step without Human Annotations.** *Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers), pp. 9426–9439. Association for Computational Linguistics*. [DOI: 10.18653/v1/2024.acl-long.510](https://doi.org/10.18653/v1/2024.acl-long.510); [arXiv:2312.08935](https://arxiv.org/abs/2312.08935).

Xinru Wang; Zhexuan Ma; Ming Yin; Shuai Ma; Thomas W. Malone. (2026). **Graphionale: How Graph Visualizations of LLM Rationales Affect Human Decision Making.** *Proceedings of the 39th Annual ACM Symposium on User Interface Software and Technology (UIST 2026)*. [DOI: 10.1145/3830398.3830638](https://doi.org/10.1145/3830398.3830638); [arXiv:2608.27932](https://arxiv.org/abs/2608.27932). Forthcoming, UIST 2026, November 2–5, Detroit, Michigan; reviewed August 28, 2026 arXiv manuscript. Publisher DOI is stated in the manuscript and arXiv record; Crossref returned no record at the review cutoff.

Sarah Wiegreffe; Jack Hessel; Swabha Swayamdipta; Mark Riedl; Yejin Choi. (2022). **Reframing Human-AI Collaboration for Generating Free-Text Explanations.** *Proceedings of the 2022 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, pp. 632–658. Association for Computational Linguistics*. [DOI: 10.18653/v1/2022.naacl-main.47](https://doi.org/10.18653/v1/2022.naacl-main.47); [arXiv:2112.08674](https://arxiv.org/abs/2112.08674).

Tongshuang Wu; Michael Terry; Carrie J. Cai. (2022). **AI Chains: Transparent and Controllable Human-AI Interaction by Chaining Large Language Model Prompts.** *CHI Conference on Human Factors in Computing Systems, pp. 1–22. ACM*. [DOI: 10.1145/3491102.3517582](https://doi.org/10.1145/3491102.3517582); [arXiv:2110.01691](https://arxiv.org/abs/2110.01691).

Tongshuang Wu; Ellen Jiang; Aaron Donsbach; Jeff Gray; Alejandra Molina; Michael Terry; Carrie J. Cai. (2022). **PromptChainer: Chaining Large Language Model Prompts through Visual Programming.** *CHI Conference on Human Factors in Computing Systems Extended Abstracts, pp. 1–10. ACM*. [DOI: 10.1145/3491101.3519729](https://doi.org/10.1145/3491101.3519729); [arXiv:2203.06566](https://arxiv.org/abs/2203.06566).

Liwenhan Xie; Chengbo Zheng; Haijun Xia; Huamin Qu; Chen Zhu-Tian. (2024). **WaitGPT: Monitoring and Steering Conversational LLM Agent in Data Analysis with On-the-Fly Code Visualization.** *Proceedings of the 37th Annual ACM Symposium on User Interface Software and Technology, pp. 1–14. ACM*. [DOI: 10.1145/3654777.3676374](https://doi.org/10.1145/3654777.3676374); [arXiv:2408.01703](https://arxiv.org/abs/2408.01703).

Catherine Yeh; Yida Chen; Aoyu Wu; Cynthia Chen; Fernanda Viégas; Martin Wattenberg. (2024). **AttentionViz: A Global View of Transformer Attention.** *IEEE Transactions on Visualization and Computer Graphics, 30(1), pp. 262–272. Institute of Electrical and Electronics Engineers (IEEE)*. [DOI: 10.1109/TVCG.2023.3327163](https://doi.org/10.1109/TVCG.2023.3327163); [arXiv:2305.03210](https://arxiv.org/abs/2305.03210).

Runtao Zhou; Giang Nguyen; Nikita Kharya; Anh Totti Nguyen; Chirag Agarwal. (2026). **Improving Human Verification of LLM Reasoning through Interactive Explanation Interfaces.** *Proceedings of the 31st International Conference on Intelligent User Interfaces, pp. 456–473. ACM*. [DOI: 10.1145/3742413.3789134](https://doi.org/10.1145/3742413.3789134); [arXiv:2510.22922](https://arxiv.org/abs/2510.22922).

## Appendix A. Coverage and Version Ledger
Every active PDF appears once below. The review numbers follow the source synthesis report. Figure numbers refer to this whitepaper. Local PDF page counts include references and appendices; they need not equal published page ranges.
| Review / part | Paper and local PDF | Reviewed version / figure |
|---|---|---|
| 1 / I | Turpin et al. (2023); `2023_Turpin_faithfulness.pdf` | arXiv 2305.04388v2; 32 PDF pages. Figure(s): No interface/concept figure required. |
| 2 / I | Lanham et al. (2023); `2023_Lanham_faithfulness.pdf` | arXiv 2307.13702v1; 14 PDF pages. Figure(s): No interface/concept figure required. |
| 3 / I | Radhakrishnan et al. (2023); `2023_Radhakrishnan_decomposition.pdf` | arXiv 2307.11768v2; 31 PDF pages. Figure(s): No interface/concept figure required. |
| 4 / I | Jacovi and Goldberg (2020); `2020_Jacovi_faithfulness.pdf` | Published ACL Anthology PDF; 8 PDF pages. Figure(s): No interface/concept figure required. |
| 5 / I | Wiegreffe et al. (2022); `2022_Wiegreffe_explanations.pdf` | Published ACL Anthology PDF; 27 PDF pages. Figure(s): 1. |
| 6 / II | Vig (2019); `2019_Vig_bertviz.pdf` | Published ACL Anthology PDF; 6 PDF pages. Figure(s): 2. |
| 7 / II | Hoover et al. (2020); `2020_Hoover_exbert.pdf` | Published ACL Anthology PDF; 10 PDF pages. Figure(s): 3. |
| 8 / II | Yeh et al. (2024); `2024_Yeh_attentionviz.pdf` | arXiv 2305.03210v2; 11 PDF pages. Figure(s): 4. |
| 9 / II | Geva et al. (2022); `2022_Geva_lmdebugger.pdf` | Published ACL Anthology PDF; 10 PDF pages. Figure(s): 5. |
| 10 / II | Belrose et al. (2023); `2023_Belrose_tunedlens.pdf` | arXiv 2303.08112v6; 25 PDF pages. Figure(s): 6. |
| 11 / II | Ghandeharioun et al. (2024); `2024_Ghandeharioun_patchscopes.pdf` | Published ICML 2024 PDF (PMLR 235); 25 PDF pages. Figure(s): 7. |
| 12 / II | Kuhn et al. (2023); `2023_Kuhn_semanticuncertainty.pdf` | arXiv 2302.09664v3; 19 PDF pages. Figure(s): No interface/concept figure required. |
| 13 / II | Lightman et al. (2024); `2024_Lightman_verify.pdf` | Published ICLR 2024 PDF; 24 PDF pages. Figure(s): 8. |
| 14 / II | Wang et al. (2024); `2024_Wang_mathshepherd.pdf` | Published ACL Anthology PDF; 14 PDF pages. Figure(s): 9. |
| 15 / III | Wu, Terry, and Cai (2022); `2022_Wu_aichains.pdf` | arXiv 2110.01691v3; 22 PDF pages. Figure(s): 10. |
| 16 / III | Wu, Jiang, et al. (2022); `2022_Wu_promptchainer.pdf` | arXiv 2203.06566v1; 10 PDF pages. Figure(s): 11. |
| 17 / III | Arawjo et al. (2024); `2024_Arawjo_chainforge.pdf` | Author-hosted CHI 2024 paper; 18 PDF pages. Figure(s): 12. |
| 18 / III | Epperson et al. (2025); `2025_Epperson_agdebugger.pdf` | Author-hosted CHI 2025 paper; 15 PDF pages. Figure(s): 13. |
| 19 / III | Kahng et al. (2024); `2024_Kahng_comparator.pdf` | Author-hosted CHI Extended Abstracts 2024 paper; 7 PDF pages. Figure(s): 14. |
| 20 / III | Xie et al. (2024); `2024_Xie_waitgpt.pdf` | Published paper / author manuscript; Proceedings of the 37th Annual ACM Symposium on User Interface Software and Technology (UIST 2024); 14 PDF pages. Figure(s): 15. |
| 21 / III | Lee et al. (2022); `2022_Lee_coauthor.pdf` | arXiv 2201.06796v2; 19 PDF pages. Figure(s): 16. |
| 22 / IV | Li et al. (2025); `2025_Li_reasongraph.pdf` | Published paper / author manuscript; ACL 2025 System Demonstrations; 8 PDF pages. Figure(s): 17. |
| 23 / IV | Liu et al. (2025); `2025_Liu_sprout.pdf` | arXiv 2312.01801v2; 15 PDF pages. Figure(s): 18. |
| 24 / IV | Chen et al. (2026); `2026_Chen_reasondiag.pdf` | arXiv 2603.21286v2; 18 PDF pages. Figure(s): 19. |
| 25 / IV | Felder et al. (2026); `2026_Felder_retrace.pdf` | arXiv 2511.11187v1; 32 PDF pages. Figure(s): 20, 21. |
| 26 / IV | Nguyen et al. (2026); `2026_Nguyen_hot.pdf` | arXiv 2503.02003v6; 54 PDF pages. Figure(s): 22. |
| 27 / V | Suh et al. (2023); `2023_Suh_sensecape.pdf` | Author-hosted UIST 2023 paper; 18 PDF pages. Figure(s): 23. |
| 28 / V | Boyle et al. (2024); `2024_Boyle_itot.pdf` | Published paper / author manuscript; IEEE VIS 2024 Workshop on Natural Language Interfaces for Visualization (NLVIZ); 8 PDF pages. Figure(s): 24. |
| 29 / V | Pang et al. (2026); `2026_Pang_hippo.pdf` | arXiv 2506.23678v1; 15 PDF pages. Figure(s): 25. |
| 30 / V | Zhou et al. (2026); `2026_Zhou_verification.pdf` | arXiv 2510.22922v4; 18 PDF pages. Figure(s): 26. |
| 31 / VI | Fernandes et al. (2026); `2026_Fernandes_explaining.pdf` | arXiv 2605.25856v1; 27 PDF pages. Figure(s): 27. |
| 32 / VI | Sun et al. (2026); `2026_Sun_seeing.pdf` | arXiv 2603.07306v2; 7 PDF pages. Figure(s): 28. |
| 33 / VI | Wang et al. (2026); `2026_Wang_graphionale.pdf` | arXiv 2608.27932v1; 21 PDF pages. Figure(s): 29. |
## Appendix B. Figure Inventory
The asset names and exact crop coordinates are recorded in `figures/provenance.json`. Each asset is a 300-dpi rasterization of an original PDF figure or selected panel. Source and asset SHA-256 hashes identify the exact inputs and outputs.
| Whitepaper figure | Source | Original figure / PDF page |
|---|---|---|
| 1 | Wiegreffe et al. (2022) | Figure 9, PDF page 26 |
| 2 | Vig (2019) | Figure 1, PDF page 2 |
| 3 | Hoover et al. (2020) | Figure 1, PDF page 2 |
| 4 | Yeh et al. (2024) | Figure 5, PDF page 5 |
| 5 | Geva et al. (2022) | Figure 2, PDF page 3 |
| 6 | Belrose et al. (2023) | Figure 1, PDF page 1 |
| 7 | Ghandeharioun et al. (2024) | Figure 1, PDF page 1 |
| 8 | Lightman et al. (2024) | Figure 1, PDF page 3 |
| 9 | Wang et al. (2024) | Figure 1, PDF page 4 |
| 10 | Wu, Terry, and Cai (2022) | Figure 3, PDF page 7 |
| 11 | Wu, Jiang, et al. (2022) | Figure 1, PDF page 2 |
| 12 | Arawjo et al. (2024) | Figure 1, PDF page 1 |
| 13 | Epperson et al. (2025) | Figure 3, PDF page 7 |
| 14 | Kahng et al. (2024) | Figure 1, PDF page 1 |
| 15 | Xie et al. (2024) | Figure 3, PDF page 6 |
| 16 | Lee et al. (2022) | Figure 3, PDF page 6 |
| 17 | Li et al. (2025) | Figure 1, PDF page 3 |
| 18 | Liu et al. (2025) | Figure 3, PDF page 7 |
| 19 | Chen et al. (2026) | Figure 2, PDF page 6 |
| 20 | Felder et al. (2026) | Figure 4, PDF page 10 |
| 21 | Felder et al. (2026) | Figure 5, PDF page 11 |
| 22 | Nguyen et al. (2026) | Figure 3, PDF page 5 |
| 23 | Suh et al. (2023) | Figure 1, PDF page 1 |
| 24 | Boyle et al. (2024) | Figure 4, PDF page 4 |
| 25 | Pang et al. (2026) | Figure 1, PDF page 4 |
| 26 | Zhou et al. (2026) | Figure 2, PDF page 5 |
| 27 | Fernandes et al. (2026) | Figure 2, PDF page 8 |
| 28 | Sun et al. (2026) | Figure 1, PDF page 2 |
| 29 | Wang et al. (2026) | Figure 1, PDF page 1 |

## Appendix C. Qualifications to the Source Synthesis Report

The supplied report determines the six-part organization and the order of the reviews. The paper-level analysis uses the PDFs as the authority for methods and results. The entries below record consequential differences between the supplied synthesis and the interpretation supported by the reviewed sources. They also identify reporting issues within a few papers where those issues affect the conclusions. Review numbers provide the route to the fuller explanation and its citation.

### Foundations, inspection, and verification

**Reviews 1–4: Faithfulness is conditional and distinct from plausibility.** The foundational experiments test particular interventions, prompt biases, models, and tasks. They do not establish that every generated chain is unused or that factored decomposition guarantees a complete account of computation. Radhakrishnan et al. evaluate model behavior rather than a human trust or error-localization interface. Jacovi and Goldberg offer a conceptual analysis of definitions and evaluation assumptions, rather than a completed numerical metric that resolves faithfulness across methods.

**Review 5: Explanation quality depends on the criterion and reference set.** Wiegreffe et al. evaluate human acceptability and selective generation. The comparisons do not show that model explanations are uniformly superior to human explanations. Results differ across datasets, reference explanations, and filtering conditions. The reproduced annotation interface is included because the judgment procedure is part of the paper's contribution.

**Reviews 6–11: Inspection and decoding are not automatically causal explanations.** Attention visualizations expose computed patterns; dimensionality reduction adds a projection whose geometry must be interpreted carefully. LM-Debugger includes intervention, while the Tuned Lens and Patchscopes decode information under their respective transformation and prompting procedures. An interpretable output from a decoding method is not, by itself, proof that the original model used the decoded statement as its reason.

**Review 12: Semantic uncertainty is not direct truth verification.** Meaning-based clustering improves uncertainty discrimination in the tested settings. Answers can nevertheless agree and be wrong. The reported AUROC results should not be described as a general calibration guarantee or a probability that an individual answer is correct.

**Reviews 13–14: Process-supervision results require their sampling conditions.** Lightman et al.'s primary comparison concerns MATH solution selection, with a fixed generator and trained reward models. The headline result uses a large best-of-sample budget; it is not a single generated answer's accuracy. GSM8K should not be substituted for the paper's primary benchmark. Math-Shepherd additionally trains generators with reinforcement learning, but its continuation-based labels remain estimates of useful or correct steps. Candidate budgets, weighted voting, verification, and reinforcement-learning conditions must remain separate when quoting results.

### Workflow and reasoning interfaces

**Reviews 15–21: System capability and measured effectiveness differ.** Several papers demonstrate a tool through case studies, formative work, or small evaluations. Their implemented interaction should not be converted into a claim of general error-reduction effectiveness. AGDebugger, for example, supports checkpoint-based intervention, while only two of eight steering participants reached the exact correct answer in the reported task. WaitGPT supports particular code operations, and its error-detection results vary by task. CoAuthor's interaction statistics are observational rather than causal estimates of writing productivity.

**Review 22: ReasonGraph does not establish a controlled comprehension gain.** The paper reports high user ratings, including a 4.9 rating, with limited detail about sampling and comparison. That rating is not 98% graph accuracy, nor evidence of a statistically established improvement in code comprehension. The system supports more reasoning methods than the four layouts emphasized in the report. Direct graph editing remains future work.

**Review 23: SPROUT's evidence concerns authors and generated links.** The system includes six coordinated views and actions for tutorial construction. The user study supports several authoring ratings, while differences in understanding, confidence, and perceived quality are not all statistically significant. Its paragraph-to-code evaluation identifies both correct and erroneous links. The study is not an evaluation of students learning from the resulting tutorials.

**Review 24: ReasonDiag's automated diagnosis favors recall.** Its reported technical evaluation has recall of 0.801 and precision of 0.306. A high number of false-positive flags is therefore part of the evidence, not an incidental possibility. Symbolic checking depends on generated translations and premises. The dependency diagram does not establish the model's internal causal reasoning, and the interface evaluation does not provide a controlled baseline showing improved objective human diagnosis.

**Review 25: ReTrace's geometric encodings have specific meanings.** The Timeline allocates width using step counts, not measured execution duration. The Space-Filling layout begins with equal phase quadrants, so those quadrants should not be read as proportional phase lengths. The human study supports selected interpretation and workload findings, but does not establish a general speed improvement or better difficult-error detection. Its correctness judgments have a ceiling. Real-time steering is outside the evaluated contribution.

**Review 26: HoT's speed result has an accuracy tradeoff.** HoT means Highlighted Chain of Thought. Its human-study comparison uses highlighted versus unhighlighted versions of the same HoT text. Mean judgment time decreases from 62.38 to 47.26 seconds, while rejection of incorrect answers decreases from 72.21% to 54.83%. Describing only the approximately one-quarter reduction in time omits the central verification tradeoff. SelfCheck consistency is also not a direct ground-truth hallucination rate. The review avoids an arithmetic aggregate in the paper whose reported baseline average is inconsistent with the displayed component values.

### Exploration and human evaluation

**Review 27: Sensecape evaluates exploratory behavior, not factual reliability.** More concepts and deeper organization do not establish better learning or more accurate conclusions. Several activity counts are not significantly different. The evaluated baseline includes both chat and a canvas, and fact checking is outside the implemented study scope.

**Review 28: iToT's demonstrations are not a controlled user study.** The paper presents illustrative workflows and model-based thought evaluations. User override is meaningful partly because the preferred model path can be wrong. The implementation fixes several settings at initialization; it should not be described as providing unrestricted adjustment of every parameter at every layer. Fully automatic solving is future work.

**Review 29: Hippo's main evidence is perceived control and awareness.** Its comparison baseline permits editing of linear reasoning. The measured gains in control and confidence do not establish improved objective answer correctness. Topic relations and explicit thought editing should not be equated with causal model-state manipulation. Branch deletion and visual collapse also have different effects and should not be collapsed into one operation called tree trimming.

**Review 30: Interactive verification is evaluated under a high error prevalence.** Zhou et al. analyze 125 participants and give each participant one correct and nine incorrect solutions. Interactive formats improve aggregate verification and localization relative to CoT in the reported analysis. The results do not establish significant differences among every pair of interactive formats or significant pairwise speed gains. A policy of always answering “incorrect” would achieve 90% binary accuracy under this trial mix, although it would not solve the localization task. Repeated omnibus statistics and inconsistent model naming in the manuscript limit confidence in finer reporting details.

**Review 31: The full-trace effect is not an isolated test of verbosity.** Fernandes et al. vary model and answer-reveal behavior across conditions as well as trace presentation. Full-trace participants perform worse than answer-only and summary-trace participants. The proposed explanation through cognitive offloading is an interpretation, not an independently established causal mechanism. Summary-trace does not show a detected performance improvement over answer-only. All groups' achieved scores exceed the models' matched five-of-ten benchmark in the reported results, despite inconsistent wording in the discussion.

**Review 32: On-demand rationales do not show the claimed significant calibration advantage.** Sun et al.'s presentation-format comparison is not statistically significant. Certainty wording and rationale correctness affect adoption, but the experiment holds final answers fixed while varying rationale properties. It contains no answer-only baseline. The source report's claim that on-demand presentation significantly improves calibration and error detection is therefore not supported by the reported experiment.

**Review 33: Graphionale's reversal is specific to tested measures and modalities.** Graphs improve over-trust and correction measures on verbal tasks while worsening several calibration measures on visual tasks. The visual-task result includes increased under-trust, so it should not be reduced to inflated trust alone. Subjective experience favors the graph in the condition with worse behavioral results. A mismatch between abstract arguments and perceptual evidence is a plausible explanation advanced by the authors, but perceptual grounding is not independently manipulated to establish that mechanism.

### Publication and version limits

The local manuscript remains the reviewed source when final publication metadata differs. AttentionViz's 2024 issue, SPROUT's 2025 issue, and the 2026 records for Hippo, ReasonDiag, ReTrace, and HoT are identified separately from local revision dates. Graphionale is a forthcoming UIST 2026 paper at the September 8 cutoff. Its DOI is supplied by the manuscript and arXiv record but did not return a Crossref record during verification. Preprints and the iToT workshop paper retain their actual status without invented proceedings pagination. These distinctions are recorded in the bibliography, coverage ledger, and accompanying reference data.
