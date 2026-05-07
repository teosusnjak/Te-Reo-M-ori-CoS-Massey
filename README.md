# A small-scale computational audit of Te Reo Māori visibility in College of Sciences publications, 2012-2022

**Draft GitHub preprint**

Teo Susnjak, Vajisha Wanniarachchi, and Anuradha Mathrani  
Massey University, Aotearoa New Zealand

## Abstract

This working paper presents a small-scale computational audit of visible Te Reo Māori usage in research publications associated with Massey University's College of Sciences. The study was developed through the College of Sciences REaDI Iwi Fund as an exploratory method for describing how Māori-language terms appear in published research outputs over time. A corpus of 1,393 publication records from 2012 to 2022 was assembled by following a selected panel of academics across three College schools: the School of Built Environment (SBE), the School of Mathematical and Computational Sciences (SMCS), and the School of Natural Sciences (SNS). Publication PDFs were organised by school, field, and year, text was extracted from the PDFs, and a rule-based natural language processing workflow was used to identify candidate Te Reo Māori words and terms. The cleaned working dataset contains 16,805 candidate term instances across 4,517 unique candidate tokens. Descriptive results indicate variation across schools and fields, with candidate term counts increasing in the later years of the corpus. However, the method also identifies false positives and cannot measure the quality, intent, or depth of Māori-language use. The contribution of this paper is therefore methodological and descriptive: it shows that a lightweight text-mining workflow can provide a preliminary view of Māori-language visibility in scientific publishing, while also identifying the validation work needed before stronger claims can be made.

**Keywords:** Te Reo Māori; Mātauranga Māori; research publications; natural language processing; language visibility; institutional research analytics; Aotearoa New Zealand

## 1. Introduction

Universities in Aotearoa New Zealand increasingly seek to understand how their research activities relate to Te Reo Māori, Mātauranga Māori, and institutional commitments to research that is meaningful in this national context. One practical challenge is measurement. Institutional reporting often captures outputs, funding, collaborations, and citations, but it less often captures the visible presence of Māori language within the published record itself.

This study addresses that practical measurement problem at a modest scale. It asks whether a computational text-mining workflow can provide a first-pass description of Te Reo Māori visibility across a selected panel of College of Sciences publication outputs at Massey University. The intent is not to judge individual publications or researchers, nor to infer the quality of engagement with Māori knowledge. Rather, the aim is to test whether a reproducible corpus and a transparent text-processing pipeline can generate useful descriptive evidence about the appearance of Māori-language terms across schools, fields, and years.

The project was conducted as an exploratory REaDI Iwi Fund activity at Massey University's College of Sciences. The original practical goal was to collect publications from selected researchers across the College, follow their outputs over approximately a decade, extract text from publication PDFs, identify candidate Māori-language terms, and visualise patterns over time. This panel-style design was intended to improve longitudinal comparability by avoiding a constantly changing researcher sample. The present GitHub preprint brings those outputs together into a single narrative: the motivation, literature context, research questions, methods, descriptive results, limitations, and future work.

The paper is deliberately cautious in its claims. The current workflow identifies candidate Māori-language tokens using rule-based text processing and filtering. Some detected tokens are genuine Māori terms, including place names and culturally meaningful concepts; others are likely false positives caused by names, acronyms, PDF extraction artefacts, short words, or non-Māori strings that resemble Māori phonotactic patterns. For this reason, the findings should be read as a preliminary audit of candidate language visibility, not as a definitive linguistic analysis.

## 2. Literature review

### 2.1 Mātauranga Māori and research in Aotearoa New Zealand

Mātauranga Māori is commonly described as a broad knowledge system that includes Māori ways of knowing, knowledge generation, values, relationships, and locally grounded understandings. Mercier (2018) emphasises that Mātauranga Māori is not simply a static archive of traditional information. It is a continuing knowledge-generating system that is connected to iwi, hapū, place, practice, and contemporary research. This distinction is important for the present study because counting Te Reo Māori terms in publications cannot, by itself, measure Mātauranga Māori. A term count can only provide one narrow indicator of visibility within written research outputs.

Broughton and McBreen (2015) similarly describe Mātauranga Māori as a complete knowledge system, with its own principles and forms of organisation. For this study, that account shapes the interpretation of results: the computational method can identify textual traces, but it cannot evaluate whether the research itself is substantively grounded in Māori knowledge systems, partnership, or local priorities. Kaiser and Saunders (2021) provide a more applied research-planning perspective. They examine Vision Mātauranga as a research policy context and argue that researchers often need clearer starting points for understanding Māori interests, priorities, and engagement pathways. Their focus on iwi and hapū management plans is useful because it highlights a practical gap between broad research-policy expectations and the everyday planning work of researchers. The current study sits in a related practical space: it does not solve the deeper question of research engagement, but it offers a descriptive tool that institutions can use to notice broad publication-level patterns.

### 2.2 Te Reo Māori visibility and language planning

The visibility of Te Reo Māori in public and institutional domains matters because language use is shaped not only by fluent speakers but also by wider social settings, norms, and attitudes. De Bres (2011) examines government efforts to promote positive attitudes and behaviours toward Te Reo Māori among non-Māori New Zealanders. Her analysis is relevant here because academic publishing is one of the institutional domains in which attitudes toward language visibility can become visible. Even when publications are written primarily in English, the presence or absence of Māori words, place names, and concepts can indicate how a research community represents its national and cultural context. Barr and Seals (2018) show that language policy is not only a matter of high-level institutional statements. In their study of mainstream New Zealand schools, teachers' identities, attitudes, capabilities, and micro-policies affected the presence of Te Reo Māori in classroom practice. While their setting is education rather than research publishing, the same general insight applies: language visibility depends on local practices and norms as much as formal commitments. In research publications, language choices may similarly reflect disciplinary conventions, author familiarity, journal expectations, and the relevance of Māori terms to the research topic. Boshier (2015) reviews Māori language revitalisation across informal, non-formal, and formal learning settings. His account is useful for situating the study historically: Te Reo Māori visibility in contemporary institutions can be read against a longer trajectory of language decline, revitalisation, policy activity, and expanding interest in language learning. This study does not evaluate language revitalisation outcomes, but it uses computational methods to observe one small domain in which language visibility can be tracked over time.

### 2.3 Multilingual academic publishing

Academic publishing is strongly shaped by English-language norms. Curry and Lillis (2024) argue that academic knowledge production is often treated as an "English Only" space, despite the multilingual realities of many research communities. Their work provides a useful international frame for this study. The question for the present paper is not whether English should disappear from scientific publishing. It is more limited: whether a local publication corpus can be examined for visible Māori-language markers in a transparent and reproducible way.

### 2.4 Gap addressed by this study

The reviewed literature supports three starting assumptions. First, Mātauranga Māori is a broad knowledge system and cannot be fully represented by term counts. Second, Te Reo Māori visibility across institutional domains is a reasonable descriptive topic because language presence is one observable part of a wider research culture. Third, academic publishing is a multilingual and locally situated activity, even when English is the dominant language of publication.

The gap addressed here is practical and methodological. We ask whether a small, transparent NLP workflow can be used to produce a descriptive baseline of candidate Te Reo Māori terms in a defined institutional publication corpus. Such a baseline cannot answer every substantive question, but it can support more informed discussion and identify where richer qualitative or validated linguistic analysis would be needed.

## 3. Research questions

The present analysis is guided by three research questions:

**RQ1.** What is the distribution of candidate Te Reo Māori terms in a selected panel of College of Sciences publication outputs from 2012 to 2022?

**RQ2.** How do candidate term counts vary across schools, fields, and years?

**RQ3.** What methodological issues arise when using automated text extraction and rule-based filtering to estimate Māori-language visibility in research publications?

These questions are intentionally descriptive. They align with the current dataset and do not require new experiments beyond the existing corpus and processing outputs.

## 4. Methodology

### 4.1 Corpus and publication scope

The working corpus consists of publication PDFs and metadata associated with a selected panel of academics in Massey University's College of Sciences from 2012 to 2022. The processed dataset used for the present draft is `Processed_Data_Cleaned_Removed.csv`, which contains 1,393 publication records.

The sampling logic is longitudinal rather than census-based. The project followed selected academics across the study period to reduce the risk that year-to-year changes were driven only by changes in who was included in the corpus. This design improves comparability across time, but it also means that the corpus should be interpreted as a panel-based sample rather than a complete institutional record of College publication activity.

The publications are grouped into three schools:

- School of Built Environment (SBE): 423 records
- School of Mathematical and Computational Sciences (SMCS): 471 records
- School of Natural Sciences (SNS): 499 records

The corpus also includes field-level labels. SBE records are distributed across Building Technology, Built Environment, Construction Management, and Quantity Surveying. SMCS records are distributed across Computer Science, Mathematics, and Statistics. SNS records are distributed across Biology, Chemistry, Genetics, Plant Science, and Zoology and Ecology.

The broader source export, `Publications_in_College_of_Sciences_2012_to_2022.xlsx`, contains a larger bibliographic dataset. The present analysis uses the subset for which PDFs were processed and cleaned in the project workflow.

### 4.2 Text extraction

Publication PDFs were organised by school, field, and year in the `datasets/CoS-Merged/` directory. The exploratory notebooks indicate that PDF text was extracted using Python, primarily through `PyPDF2`, and then tokenised using regular-expression based word extraction. The extraction process attempted to remove common PDF artefacts such as hyphenation across line breaks.

PDF extraction quality is a known limitation. Some PDFs contain encoding artefacts, split words, tables, headers, footers, reference lists, and publisher metadata. These features can affect both the total extracted text and the candidate Māori-term list.

### 4.3 Candidate Māori-term detection

The notebooks define Māori orthographic character sets and use rule-based filtering to identify words that may plausibly be Māori. The process includes:

1. extracting words from each PDF;
2. normalising or processing text for matching;
3. comparing tokens against Māori-like word patterns and candidate vocabularies;
4. removing known false positives and stop words through a later cleaning pass;
5. saving publication-level candidate term lists in CSV form.

The final compact dataset used here stores candidate terms in a `Maori_words` column. For each publication, candidate terms were split on commas and counted as candidate term instances.

### 4.4 Descriptive analysis

The analysis in this paper is descriptive. We counted:

- number of publication records by school, field, and year;
- number of records containing at least one candidate term;
- total candidate term instances by school, field, and year;
- mean candidate term instances per publication record;
- most frequent candidate tokens in the cleaned dataset.

No inferential statistical tests are reported in this draft. Given the exploratory nature of the corpus and the known false-positive problem, inferential claims would be premature.

## 5. Results

### 5.1 Corpus composition

The cleaned working dataset contains 1,393 publication records across 2012-2022. Table 1 summarises the distribution by school.

**Table 1. Publication records by school**

| School | Publication records |
|---|---:|
| SBE | 423 |
| SMCS | 471 |
| SNS | 499 |
| **Total** | **1,393** |

The number of publication records increases in the later years of the corpus, with 188 records in 2022 compared with 97 in 2012. This reflects the composition of the assembled researcher-panel corpus and should not automatically be interpreted as a change in College publication productivity or in the publication behaviour of the wider College.

**Table 2. Publication records by year**

| Year | Publication records |
|---:|---:|
| 2012 | 97 |
| 2013 | 103 |
| 2014 | 94 |
| 2015 | 93 |
| 2016 | 133 |
| 2017 | 110 |
| 2018 | 116 |
| 2019 | 151 |
| 2020 | 154 |
| 2021 | 154 |
| 2022 | 188 |

### 5.2 Candidate term counts by school

The cleaned dataset contains 16,805 candidate term instances. Table 3 summarises the school-level distribution.

**Table 3. Candidate Te Reo Māori term instances by school**

| School | Records | Records with candidate terms | Candidate instances | Mean candidate instances per record |
|---|---:|---:|---:|---:|
| SBE | 423 | 394 | 5,460 | 12.91 |
| SMCS | 471 | 430 | 4,651 | 9.87 |
| SNS | 499 | 474 | 6,694 | 13.41 |
| **Total** | **1,393** | **1,298** | **16,805** | **12.06** |

SNS has the largest total number of candidate instances, followed by SBE and SMCS. Mean candidate instances per record are similar for SNS and SBE, while SMCS has a lower mean. These results should be interpreted cautiously because the counts are not normalised by full publication length and still contain likely false positives.

![Māori word count summary by year and school](words_by_school.png)

### 5.3 Candidate term counts by year

Candidate term instances are higher in the later part of the corpus. The mean count per record rises from 9.41 in 2012 to 17.66 in 2022.

**Table 4. Candidate term instances by year**

| Year | Records | Candidate instances | Mean candidate instances per record |
|---:|---:|---:|---:|
| 2012 | 97 | 913 | 9.41 |
| 2013 | 103 | 1,023 | 9.93 |
| 2014 | 94 | 622 | 6.62 |
| 2015 | 93 | 662 | 7.12 |
| 2016 | 133 | 1,306 | 9.82 |
| 2017 | 110 | 1,164 | 10.58 |
| 2018 | 116 | 1,522 | 13.12 |
| 2019 | 151 | 1,919 | 12.71 |
| 2020 | 154 | 1,892 | 12.29 |
| 2021 | 154 | 2,462 | 15.99 |
| 2022 | 188 | 3,320 | 17.66 |

This pattern is consistent with increased candidate Māori-language visibility over time within the assembled panel corpus, but the current method cannot determine the cause. Possible explanations include changes in publication topics, more frequent use of Aotearoa New Zealand place names, changes in author practice, staff turnover effects within the original tracked group, or genuine increased use of Māori terms.

![Candidate words by year and school](by_year_school.png)

### 5.4 Candidate term counts by field

Field-level results show substantial variation. Zoology and Ecology, Construction Management, Plant Science, and Statistics have relatively high mean candidate counts per record in the current dataset, while Computer Science and Building Technology have lower means.

**Table 5. Candidate term instances by school and field**

| School | Field | Records | Candidate instances | Mean per record |
|---|---|---:|---:|---:|
| SBE | Building_Technology | 94 | 648 | 6.89 |
| SBE | Built_Environment | 119 | 1,402 | 11.78 |
| SBE | Construction_Management | 177 | 3,009 | 17.00 |
| SBE | Quantity_Surveying | 33 | 401 | 12.15 |
| SMCS | Computer Science | 185 | 1,233 | 6.66 |
| SMCS | Mathematics | 123 | 978 | 7.95 |
| SMCS | Statistics | 163 | 2,440 | 14.97 |
| SNS | Biology | 208 | 2,959 | 14.23 |
| SNS | Chemistry | 107 | 925 | 8.64 |
| SNS | Genetics | 64 | 626 | 9.78 |
| SNS | Plant_Science | 40 | 667 | 16.68 |
| SNS | Zoology_and_Ecology | 80 | 1,517 | 18.96 |

Field differences are plausible because some disciplines more often publish work involving New Zealand species, ecosystems, places, communities, or policy contexts. However, a validated analysis would need to separate genuine Māori-language terms from author names, place names, institution names, and extraction artefacts.

### 5.5 Frequently detected candidate tokens

The most frequent candidate tokens include a mixture of meaningful terms and likely false positives. Recognisable examples include `aotearoa`, `waikato`, `mana`, `manawatu`, `rotorua`, `porirua`, `maori`, `taranaki`, and `niwa`. The list also includes short strings or names such as `ea`, `pone`, `puri`, `ure`, `noti`, and `tanaka`, which may not represent meaningful Te Reo Māori usage in context.

![Most frequent candidate Māori terms](frequency.png)

This result is important because it shows both the promise and the limits of the automated method. Frequent-token visualisations are useful for quickly inspecting the corpus, but they require manual validation before being used as evidence of substantive language use.

## 6. Discussion

### 6.1 What the results support

The current findings support a modest but useful conclusion: a computational workflow can produce a preliminary map of candidate Te Reo Māori visibility across a defined panel-based publication corpus. The dataset shows that candidate Māori-language terms are not evenly distributed across schools, fields, or years. The later years of the corpus contain higher mean candidate counts per publication record, and some fields have higher observed candidate counts than others.

These patterns are useful for institutional reflection, provided that they are interpreted as panel-based observations rather than College-wide prevalence estimates. They can help identify where Māori-language terms appear more frequently in the sampled published record and where closer reading may be warranted. The approach can also support future improvements in corpus construction, dictionary development, and validation procedures.

### 6.2 What the results do not support

The results do not show the quality or depth of engagement with Te Reo Māori or Mātauranga Māori. A paper may contain Māori terms only in a place name, author affiliation, species context, or reference title. Conversely, a paper may engage substantively with Māori communities or Māori priorities while using relatively few Māori words. Term counts therefore cannot be treated as a measure of research quality, partnership, cultural relevance, or scholarly contribution.

The results also do not provide a fully validated measure of Te Reo Māori usage. The candidate detection process is sensitive to false positives. Some false positives arise because Māori words can be short, because extracted PDF tokens can be fragmented, and because names from many languages can resemble Māori-like letter patterns. A future version of the analysis should include manual validation, stronger dictionaries, part-of-document filtering, and normalisation by total extracted word count.

### 6.3 Interpreting language visibility neutrally

The literature suggests that language visibility in institutional domains is a legitimate object of study. Mercier (2018) and Broughton and McBreen (2015) show that Mātauranga Māori is broader than textual markers, while de Bres (2011) and Barr and Seals (2018) show that attitudes, policies, and local practices shape the presence of Te Reo Māori in public and educational settings. Curry and Lillis (2024) place academic publishing within a wider multilingual context.

This study applies those ideas cautiously to research publications. It does not assume that more Māori words automatically means better research. It also does not assume that low counts indicate a problem or a lack of relevance. It is not an assessment of policy compliance, researcher performance, or publication quality. Instead, it treats visible language use as one descriptive signal among many possible signals. The value of the audit lies in establishing a transparent baseline and making the method open to improvement.

### 6.4 Practical implications

For College or university research planning, the workflow could be useful in four ways.

First, it can help institutions understand broad publication-level patterns without relying only on anecdotal impressions. Second, it can identify fields or years that may warrant closer qualitative review. Third, it can support the development of better Māori-language dictionaries and filtering tools for research analytics. Fourth, it can provide a reproducible method that can be refined by researchers, language experts, and institutional stakeholders.

For publication and reporting, the most important implication is interpretive care. A small text-mining audit can open a conversation, but it should not be used as a ranking tool or as a substitute for expert review.

## 7. Limitations

This study has several limitations.

1. The corpus is a working subset of College publications, not a complete census of all College outputs.
2. The corpus was constructed around a selected panel of academics followed over time. This improves longitudinal comparability but limits claims about the whole College.
3. Staff turnover creates a specific constraint for expansion. By the later years of the dataset, some originally tracked academics were no longer current members of the University or College. Adding replacement researchers would improve current coverage but would also change the composition of the panel, making longitudinal comparisons harder to interpret.
4. PDF text extraction can introduce errors, including broken words, headers, footers, reference-list noise, and encoding artefacts.
5. The candidate Māori-term detection method is rule-based and contains false positives.
6. Counts are not yet normalised by total extracted word count or publication length.
7. The analysis does not distinguish between titles, abstracts, body text, references, acknowledgements, affiliations, or metadata.
8. The analysis does not distinguish between Māori words, place names, personal names, organisational names, species names, or unrelated tokens.
9. The study does not measure the quality, intent, or context of Māori-language use.

These limitations are not reasons to discard the work. They define the appropriate scope of the paper: an exploratory baseline and methods note.

## 8. Future work

The next stage of the work should prioritise methodological validation and richer linguistic modelling rather than simply expanding the corpus. Corpus expansion is itself a methodological decision because the current study used a selected researcher panel to preserve longitudinal comparability. A future study would need to decide whether to retain the original panel, refresh the panel to reflect current staffing, or move to a different design such as a full College-wide publication census. Each option would answer a different research question. A useful first analytic step would be to construct a manually annotated validation sample in which candidate terms are coded as Māori lexical items, place names, personal names, organisational names, species names, or false positives. This would allow the workflow to report standard information-retrieval measures such as precision, recall, and F1 score, and would make the uncertainty in the current estimates explicit.

Future analysis could also move beyond raw counts. Candidate-term frequencies should be normalised by total extracted word count, publication length, and document section. Separating titles, abstracts, body text, acknowledgements, affiliations, and reference lists would make it possible to distinguish incidental mentions from terms that appear in the substantive argument of a paper. Named-entity recognition and gazetteer matching could help separate iwi, hapū, region, institution, and personal names from more general lexical usage. A curated Te Reo Māori lexicon, combined with exclusion lists and part-of-speech information where available, would improve the reliability of the candidate-detection stage. More interpretive extensions are also possible. Topic modelling methods such as latent Dirichlet allocation or BERTopic could be used to examine whether publications with higher candidate-term density cluster around particular research themes. Embedding-based similarity models could compare publications with Māori-language markers to the broader corpus to identify neighbouring topical areas. Time-series or change-point analysis could test whether the apparent increase in later years reflects a gradual trend or specific shifts in corpus composition. Finally, a small qualitative review of high-count publications would provide an important check on the computational results by examining how the terms are used in context. These extensions would support a more mature version of the study while preserving the transparency of the current workflow. The aim would not be to replace expert interpretation with automated classification, but to develop a more reliable descriptive framework for studying Māori-language visibility in institutional research outputs.

## 9. Conclusion

This paper brought together a small-scale corpus, computational workflow, and preliminary results on visible Te Reo Māori usage in College of Sciences publications from 2012 to 2022. The cleaned working dataset contains 1,393 publication records and 16,805 candidate Māori-language term instances. Candidate counts vary by school, field, and year, with higher mean counts appearing in the later years of the corpus.

The central contribution is not a definitive measurement of Te Reo Māori or Mātauranga Māori in research. It is a practical demonstration that institutional publication data can be used to produce an initial descriptive baseline of Māori-language visibility. Used carefully, this kind of audit can support more informed discussion, better methods, and more targeted future analysis.

## Data and materials

This repository contains the public-facing figures and processed datasets used for the exploratory analysis. The main compact dataset is available under `datasets/Processed_Data_Cleaned_Removed.csv`. The figures shown in this paper are included in the repository root.

## Acknowledgements

This work was supported by the College of Sciences REaDI Iwi Fund at Massey University. The authors acknowledge the colleagues who contributed to data collection, PDF processing, and preliminary analysis.

## References

Barr, S., & Seals, C. A. (2018). He reo for our future: Te Reo Māori and teacher identities, attitudes, and micro-policies in mainstream New Zealand schools. *Journal of Language, Identity & Education, 17*(6), 434-447. https://doi.org/10.1080/15348458.2018.1505517

Boshier, R. (2015). Learning from the moa: The challenge of Māori language revitalization in Aotearoa/New Zealand. In W. J. Jacob, S. Y. Cheng, & M. K. Porter (Eds.), *Indigenous education: Language, culture and identity*. Springer. https://doi.org/10.1007/978-94-017-9355-1_11

Broughton, D., & McBreen, K. (2015). Mātauranga Māori, tino rangatiratanga and the future of New Zealand science. *Journal of the Royal Society of New Zealand, 45*(2), 83-88. https://doi.org/10.1080/03036758.2015.1011171

Curry, M. J., & Lillis, T. (2024). Multilingualism in academic writing for publication: Putting English in its place. *Language Teaching, 57*(1), 87-100. https://doi.org/10.1017/S0261444822000040

de Bres, J. (2011). Promoting the Māori language to non-Māori: Evaluating the New Zealand government's approach. *Language Policy, 10*, 361-376. https://doi.org/10.1007/s10993-011-9214-7

Kaiser, L. H., & Saunders, W. S. A. (2021). Vision Mātauranga research directions: Opportunities for iwi and hapū management plans. *Kōtuitui: New Zealand Journal of Social Sciences Online, 16*(2), 371-383. https://doi.org/10.1080/1177083X.2021.1884099

Mercier, O. R. (2018). Mātauranga and science. *New Zealand Science Review, 74*(4), 83-90.
