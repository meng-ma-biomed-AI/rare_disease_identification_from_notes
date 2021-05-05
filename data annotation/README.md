The annotated data are available in [`Rare disease annotations from 312 MIMIC-III discharge summaries.csv`]().

## Data sampling and annotation procedure
* (i) Randomly sampled 500 discharge summaries (DS) from MIMIC-III

* (ii) 312 of the 500 DS have at least one positive UMLS mention linked to ORDO, as identified by SemEHR; there are altogether 1073 UMLS (or ORDO) mentions.

* (iii) 3 medical informatics researchers (staff or PhD) annotated the 1073 mentions, regarding whether they are the correct patient phenotypes matched to UMLS and ORDO. Contradictions resolved by another research staff having biomedical background.

## Data dictionary
| Column   Name                                | Description                                                                                                                                                                                                   |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ROW_ID                                       | Identifier unique to each row, see https://mimic.physionet.org/mimictables/noteevents/                                                                                                                                                     |
| SUBJECT_ID                                | Identifier unique to a patient, see https://mimic.physionet.org/mimictables/noteevents/                                                                                                                                                                                                              |
| HADM_ID                                      | Identifier unique to a patient hospital stay, see https://mimic.physionet.org/mimictables/noteevents/                                                                                                                                                                                                              |
| document   structure name                    | The document structure name of the mention. The document structure name is identified by   SemEHR.                                                                                                          |
| document   structure offset in full document | The start and endding offset of the document structure texts (or template) in the whole discharge summary. The document structure is parse by SemEHR with regular expressions.                            |
| mention                                      | The mention identified by SemEHR.                                                                                                                                                                          |
| mention offset in document structure       | The start and endding offset of the mention in the document structure.                                                                                                                                      |
| mention offset in full document            | The start and endding offset of the mention in the whole discharge summary. This can be calculated   by column E and G.                                                                                     |
| UMLS with desc                               | The UMLS identified by SemEHR, corresponding to the mention.                                                                                                                                                |
| ORDO with desc                               | The ORDO matched to the UMLS, using the linkage in the ORDO ontology, see   https://www.ebi.ac.uk/ols/ontologies/ordo/terms?iri=http%3A%2F%2Fwww.orpha.net%2FORDO%2FOrphanet_3325  as an example.          |
| gold mention-to-UMLS label                 | Whether the mention-UMLS pair indicate a correct phenotype of the patient (i.e. a positive mention that correctly matches to the UMLS concept), 1 if correct, 0   if not.                                 |
| gold UMLS-to-ORDO label                    | Whether the matching is correct from the UMLS concept to the ORDO concept, 1 if correct, 0 if not.                                                                                                          |
| gold mention-to-ORDO label                 | Whether the mention-ORDO triple indicates a correct phenotype of the patient, 1 if correct, 0 if not. This column is 1 if both the mention-to-UMLS label and the UMLS-to-ORDO label are 1, otherwise 0. |

**Note:**
*This annotation is by no means a perfect one; also, it is based on the output of [SemEHR](https://github.com/CogStack/CogStack-SemEHR) so it may not cover all rare diseases mentions from the sampled discharge summaries.
*An error: the row 323 is wrong due to issue in extracting the mention, the mention `nph` is not in the document structure, thus the `gold mention-to-UMLS label` is `-1`.