Data was downloaded on 2023-04-27 from SRA's BigQuery table https://www.ncbi.nlm.nih.gov/sra/docs/sra-bigquery/

SRA metadata for the top 5 pathogens by burden were downloaded to CSV and gzipped using the following query:
```SELECT
  acc,
  assay_type,
  center_name,
  consent,
  experiment,
  sample_name,
  instrument,
  platform,
  sample_acc,
  biosample,
  organism,
  sra_study,
  releasedate,
  bioproject,
  library_name,
  collection_date_sam,
  geo_loc_name_country_calc,
  geo_loc_name_country_continent_calc
FROM
  nih-sra-datastore.sra.metadata
WHERE
  assay_type = "WGS"
  AND organism IN ("Mycobacterium tuberculosis",
    "Staphylococcus aureus",
    "Escherichia coli",
    "Streptococcus pneumoniae",
    "Pseudomonas aeruingoas",
    "Klebsiella pneumoniae")
LIMIT
  10000000000000;```


Similarly all the non-human SRA WGS metadata was downloaded then xzipped to get under github's 100m limit:

```SELECT
  acc,
  assay_type,
  center_name,
  consent,
  experiment,
  sample_name,
  instrument,
  platform,
  sample_acc,
  biosample,
  organism,
  sra_study,
  releasedate,
  bioproject,
  library_name,
  collection_date_sam,
  geo_loc_name_country_calc,
  geo_loc_name_country_continent_calc
FROM
  nih-sra-datastore.sra.metadata
WHERE
  assay_type = "WGS"
  AND organism NOT IN ("Homo sapiens")
LIMIT
  10000000000000;```
