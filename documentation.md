# SWENER-1800: GLiNER2.5 fine-tuning vs. baselines
Dataset: [Riksarkivet/swener_1800](https://huggingface.co/datasets/Riksarkivet/swener_1800)

## Results (HF eval split)
- ScandiNER: 512-token windows, stride 64
- GLiNER2.5: chunk 128 words, overlap 32

### PER/LOC/ORG per label (eval, F1 strict / relaxed)
|  | ScandiNER | GLiNER2.5 baseline | GLiNER2.5 fine-tuned |
|---|---|---|---|
avg|0.272 / 0.477 |0.466 / 0.666 |0.718 / 0.842|

| Label | GT | ScandiNER | GLiNER2.5 baseline | GLiNER2.5 fine-tuned |
|---|---|---|---|---|
| PER | 2488 | 0.330 / 0.680 | 0.487  / 0.776| **0.785 / 0.947** |
| LOC | 1350 | 0.392 / 0.575 | 0.519 / 0.760 | **0.723 / 0.875** |
| ORG | 455 | 0.094 / 0.177 | 0.391 / 0.461 | **0.645 / 0.705** |


#### ScandiNER

|label | gt	| predicted | P_strict	| R_strict	| F1_strict	| P_relax |	R_relax	| F1_relax |
|---|---|---|---|---|---|---|---|---|
|PER	|2488	|1505	|0.437	|0.264	|0.330	|0.915	|0.541|	0.680|
|LOC	| 1350	| 723	| 0.562	| 0.301	| 0.392	| 0.842	| 0.436	| 0.575|
|ORG	|455	|97|	0.268	|0.057	|0.094	|0.619	|0.103	|0.177|

ScandiNER precision is reasonable but recall is low: it finds roughly a quater (strict matching) up to an half (relaxed matching) of the GT entities.

#### GLiNER2.5 baseline
|label|	gt|	predicted|	P_strict|	R_strict|	F1_strict|	P_relax|	R_relax|	F1_relax|
|---|---|---|---|---|---|---|---|---|
|	PER|	2488|	2797|	0.460|	0.517|	0.487|	0.730|	0.828|	0.776|
|	LOC|	1350|	1758|	0.458|	0.597|	0.519|	0.700|	0.832|	0.760|
|	ORG|	455|	486|	0.379|	0.404|	0.391|	0.447|	0.477|	0.461|


#### GLiNER2.5 fine-tuned
|label|	gt|	predicted|	P_strict|	R_strict|	F1_strict|	P_relax|	R_relax|	F1_relax|
|---|---|---|---|---|---|---|---|---|
|PER|	2488|	2439|	0.793|	0.778|	0.785|	0.949|	0.946|	0.947|
|LOC|	1350|	1360|	0.721|	0.726|	0.723|	0.877|	0.873|	0.875|
|ORG|	455	|469|	0.635|	0.655|	0.645|	0.693|	0.716|	0.705|


### All labels per label with GLiNER (eval, F1 strict / relaxed)
| | GLiNER2.5 baseline | GLiNER2.5 fine-tuned |
|---|---|---|
avg|0.199 / 0.316 |0.469 / 0.593|

| Label | GT | GLiNER2.5 baseline | GLiNER2.5 fine-tuned|
|---|---|---|---|
| PER | 2488 |0.467 / 0.742 |**0.774 / 0.937** |
| LOC | 1350 |0.443 / 0.697 |**0.724 / 0.873** |
| ORG-COMP | 69|0.152 / 0.277 |**0.304 / 0.475** |
| ORG-INST | 365 |0.026 / 0.032 |**0.688 / 0.736** |
| ORG-OTH | 21 |0.000 / 0.000 | **0.105 / 0.105** |
| EVN | 60 |0.026 / 0.026 | **0.333 / 0.458** |
| MSR-AREA | 12 |0.353 / 0.353 |**0.375 / 0.375** |
| MSR-DIST | 8 |0.222 / 0.556 |**0.500 / 0.750**|
| MSR-LEN | 9 |0.062 / 0.265 | **0.333 / 0.333**|
| MSR-MON | 471 |0.529 / 0.684 |**0.725 / 0.941** |
| MSR-OTH |  20 |0.000 / 0.000| 0.000 / 0.000 |
| MSR-VOL | 47 |0.233 / 0.311 | **0.518 / 0.541** |
| MSR-WEI | 15 |0.320 / 0.400 |**0.480 / 0.640** |
| OCC | 1065 |0.490 / 0.528 |**0.826 / 0.859** |
| SYMP | 48 |0.310 / 0.310 | **0.400 / 0.425**|
| TME-DATE | 777 |0.142 / 0.760 |**0.764 / 0.877** | 
| TME-INTRV | 9 |0.000 / 0.054 |0.000 / **0.500** |
| TME-TIME | 215 |0.009 / 0.017 |**0.676 / 0.827** |
| WRK | 160 |0.000 / 0.000 | **0.395 / 0.609**|


#### GLiNER2.5 baseline
|label|	gt|	predicted|	P_strict|	R_strict|	F1_strict|	P_relax|	R_relax|	F1_relax|
|---|---|---|---|---|---|---|---|---|
|PER	|2488	|3107|	0.420|	0.525|	0.467|	0.666|	0.839|	0.742|
|LOC|	1350|	2478|	0.342|	0.627|	0.443|	0.571|	0.895|	0.697|
|ORG-COMP|	69	|23	|0.304|	0.101|	0.152|	0.522|	0.188|	0.277|
|ORG-INST|	365	|14	|0.357|	0.014|	0.026|	0.429|	0.016|	0.032|
|ORG-OTH|	21	|0	|0.000|	0.000|	0.000|	0.000|	0.000|	0.000|
|EVN|	60	|17	|0.059|	0.017|	0.026|	0.059|	0.017|	0.026|
|MSR-AREA	|12|	5|	0.600|	0.250|	0.353|	0.600|	0.250|	0.353|
|MSR-DIST|	8	|10	|0.200|	0.250|	0.222|	0.500|	0.625|	0.556|
|MSR-LEN|	9	|23	|0.043|	0.111|	0.062|	0.174|	0.556|	0.265|
|MSR-MON|	471	|486|	0.521|	0.537|	0.529|	0.681|	0.688|	0.684|
|MSR-OTH|	20	|5	|0.000|	0.000|	0.000|	0.000|	0.000|	0.000|
|MSR-VOL|	47	|56	|0.214|	0.255|	0.233|	0.286|	0.340|	0.311|
|MSR-WEI|	15	|10	|0.400|	0.267|	0.320|	0.500|	0.333|	0.400|
|OCC	|1065	|660|	0.641|	0.397|	0.490|	0.691|	0.427|	0.528|
|SYMP	|48	|36	|0.361|	0.271|	0.310|	0.361|	0.271|	0.310|
|TME-DATE|	777|	617|	0.160|	0.127|	0.142|	0.874|	0.673|	0.760|
|TME-INTRV|	9|	177|	0.000|	0.000|	0.000|	0.028|	0.556|	0.054|
|TME-TIME|	215|	20|	0.050|	0.005|	0.009|	0.100|	0.009|	0.017|
|WRK	|160|	8|	0.000|	0.000|	0.000|	0.000|	0.000|	0.000|

#### GLiNER2.5 fine-tuned
|label|	gt|	predicted|	P_strict|	R_strict|	F1_strict|	P_relax|	R_relax|	F1_relax|
|---|---|---|---|---|---|---|---|---|
|PER|	2488|	2322|	0.801|	0.748|	0.774	|0.957	|0.918	|0.937|
|ORG-COMP|	69|	43|	0.395	|0.246	|0.304	|0.605	|0.391|	0.475|
|	ORG-INST|	365|	382|	0.673|	0.704	|0.688	|0.720	|0.753|	0.736|
|ORG-OTH|	21|	17|	0.118	|0.095	|0.105|	0.118|	0.095|	0.105|
|LOC|	1350|	1331	|0.730|	0.719|	0.724|	0.881	|0.865|	0.873|
|EVN|	60|	36	|0.444	|0.267|	0.333|	0.611|	0.367	|0.458|
|MSR-AREA|	12|	4	|0.750	|0.250	|0.375	|0.750	|0.250|	0.375|
|MSR-DIST|	8|	8	|0.500	|0.500	|0.500	|0.750	|0.750|	0.750|
|MSR-LEN|	9|	3	|0.667	|0.222	|0.333	|0.667	|0.222|	0.333|
|MSR-MON|	471|	462|	0.732	|0.718	|0.725	|0.950|	0.932|	0.941|
|MSR-OTH|	20|	0	|0.000	|0.000	|0.000	|0.000	|0.000|	0.000|
|MSR-VOL|	47|	38|	0.579	|0.468	|0.518	|0.605	|0.489|	0.541|
|MSR-WEI|	15|	10|	0.600	|0.400	|0.480	|0.800	|0.533|	0.640|
|OCC|	1065|	1135|	0.801|	0.854	|0.826	|0.832	|0.887	|0.859|
|SYMP|	48|	32|	0.500	|0.333|	0.400|	0.531	|0.354	|0.425|
|TME-DATE|	777|	818|	0.744|	0.784|	0.764|	0.855|	0.901|	0.877|
|TME-INTRV|	9|	3|	0.000	|0.000|	0.000|	1.000|	0.333|	0.500|
|TME-TIME|	215|	270|	0.607|	0.763|	0.676|	0.741|	0.935|	0.827|
|WRK|	160|	144|	0.417	|0.375|	0.395	|0.639|	0.581|	0.609|


## Method

**Evaluation** 
- Strict = exact span and label
- Relaxed = at least one overlapping character and the same label (not one-to-one, so it slightly overestimates)

**Splits** 
- dev set was split off from train set (10%, seed 42) leaving 610 train / 67 dev documents 
- inference chunk size was chosen on dev

**Training data conversion (GLiNER2 format)** 
- trainer takes mention strings per label, not offsets, and labels every occurrence of a string within an example (token-level, case-insensitive)
- sentence-packed chunks of up to 128 words, does not cut inside a GT span
- Result: 610 train documents totaling 4,365 chunks with 24,148 annotated spans
- Every chunk lists all 19 labels (empty list when absent)

**Training**
- `gliner2` 2.0.0, `fastino/gliner2.5-multi-v1`, fp32. 5 epochs, batch 4 x 4 accumulation, eval every 270 steps
- Best checkpoint at step 1350

## Notes
- Single training run
- Rare labels (MSR-AREA/DIST/LEN/OTH, TME-INTRV, ORG-OTH) have too few instances for reliable per-label numbers
- GLiNER used plain names ("person", "institution", ...) from SWENER-1800 documentation; prompt wording was not tuned

- errors: mostly span boundaries (compare strict vs relaxed F1), ambiguous labels (e.g. occupations) but ofc also false recognitions (LOC names as PER names etc.)
