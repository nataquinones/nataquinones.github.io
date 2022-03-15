---
layout: post
title:  "How to add annotations from a table to a GenBank file"
date:   2022-02-14 01:10:00
categories: blog
---

Say you have a table of features for a specific genome, for instance, those provided by [IslandViewer 4](https://www.pathogenomics.sfu.ca/islandviewer/), and you want to add them to your own genome in GenBank format. (I say _table_, but this obviously applies for any list of features that includes appropriate genome coordinates.) Maybe they are even features that you discovered and you generated a `tsv` with them, but the point is that you don't want to write the whole `genbank` file from scratch.

[Biopython](https://biopython.org) has a very comprehensive parser to deal with GenBank format, so this task becomes super simple. As an example, let's say we want to add the islands detected by IslandViewer4 into the original NCBI's genbank file.

- `NC_008463.1.gb`: GenBank file for [NC_008463.1 in NCBI](https://www.ncbi.nlm.nih.gov/nuccore/NC_008463.1)
- `NC_008463.1.tsv`: Results for [`NC_008463.1`'s in IslandViewer4](https://www.pathogenomics.sfu.ca/islandviewer/accession/NC_008463.1/) 
- _(You can download all these example files from [here]() if your want to follow the example.)_


## Read and process **IslandViewer 4**'s tsv file
``` python
# read file
df_iv = pd.read_csv('NC_008463.1.tsv',
                    sep='\t')

# subset only first two columns
df_iv = df_iv[['Island start', 'Island end']]

# rename columns for ease
df_iv.columns = ['start', 'end']

# remove redundant lines, here I'm interested in the "big" 
# island regions, which are specified in the first column,
# not in the individual features
df_features = df_iv.drop_duplicates(keep='first')
```

## Read reference `genbank` file
```python
# my file has a single genbank record, so I can get the object like this:
record = list(SeqIO.parse('NC_008463.1.gb', 'genbank'))[0]
```

## Add features from IslandViewer table
```python
# counter for naming (features don't have names in this table)
i = 1

# iterate over each row
for column, row in df_features.iterrows():
    # properties for the feature
    name = f'island_{str(i).zfill(2)}'
    start = row['start']
    end = row['end']
    
    # build biopython feature
    feat = SeqFeature(FeatureLocation(int(start),int(end)),
                      type='misc_feature',
                      qualifiers={'label':name})
    
    # append new features to SeqRecord object
    record.features.append(feat)
               
    # update counter
    i += 1
```

## Save
``` python
# save new file
SeqIO.write(record, 'NC_008463.1.withislands.gb', 'genbank')
```

TA DA!

