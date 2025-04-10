
# Querying for metadata

## Querying with Keys and Values
Metadata from JSON files can be queried using layout.get_metadata and the directory path. It will return a dictionary with keys and values.


````{tab-set}
```{tab-item} MEG

    metadata = layout.get_metadata(layout.get(task='induction', suffix='meg',return_type='filename')[3])

    print("metadata: ", list(metadata.keys()))
    print("Value of Dewar position: ", metadata['DewarPosition'])

    #Output:
    #metadata:  ['AssociatedEmptyRoom', 'CapManufacturer',
    #'CapManufacturersModelName', 'ContinuousHeadLocalization',
    #'DeviceSerialNumber', 'DewarPosition', 'DigitizedHeadPoints',
    #'DigitizedLandmarks', 'ECGChannelCount', 'ECOGChannelCount',
    #'EEGChannelCount', 'EEGPlacementScheme', 'EEGReference',
    #'EMGChannelCount', 'EOGChannelCount', 'EpochLength',
    #'HeadCoilFrequency', 'InstitutionAddress', 'InstitutionName',
    #'InstitutionalDepartmentName', 'Instructions', 'MEGChannelCount',
    #'MEGREFChannelCount', 'Manufacturer', 'ManufacturersModelName',
    #'MiscChannelCount', 'PowerLineFrequency', 'RecordingDuration',
    #'RecordingType', 'SEEGChannelCount', 'SamplingFrequency',
    #'SoftwareFilters', 'SoftwareVersions', 'SubjectArtefactDescription',
    #'TaskDescription', 'TaskName', 'TriggerChannelCount', 'Description',
    #'RawSources', 'Authors', 'BaselineCorrection', 'BaselineCorrectionMethod',
    #'BaselinePeriod']
    #Value of Dewar position: 'upright'

```

```{tab-item} MRI

    metadata = layout.get_metadata(layout.get(task='mixedgamblestask', suffix='bold',return_type='filename')[3])

    print("metadata: ", list(metadata.keys()))
    print("Value of RepetitionTime: ", metadata['RepetitionTime'])

    #Output:
    #metadata:  ['RepetitionTime', 'TaskName', 'SliceTiming']
    #Value of RepetitionTime:  2.0

```
````

## Querying with Suffixes
Beyond timeseries data ('meg' or 'bold'), with specific **suffix** parameter we can retrieve other files defined by the **BIDS standard**. 

```{admonition} Common suffixes in MEG data:

* **events:** search for event files, which contains time_stamps and event markers.
* **coordystem:** search for the file specifying the coordinate system used in the recording.
* **channels:** search for the file which specifies channel names and types.
* **scans:** search for the files documenting the different scan sequences that were run.

```

Here are some examples of how to query for theses BIDS specific files. 


````{tab-set}
```{tab-item} MEG

    all_events = layout.get(suffix='events',return_type='filename')
    print(all_events)

    #Output
    #['./ancp-bids/tests/data/ds003483/sub-009/ses-1/meg/sub-009_ses-1_task-deduction_run-1_events.tsv',
    #'./ancp-bids/tests/data/ds003483/sub-009/ses-1/meg/sub-009_ses-1_task-induction_run-1_events.tsv',
    #...
    #'./ancp-bids/tests/data/ds003483/sub-031/ses-1/meg/sub-031_ses-1_task-deduction_run-1_events.tsv',
    #'./ancp-bids/tests/data/ds003483/sub-031/ses-1/meg/sub-031_ses-1_task-induction_run-1_events.tsv']

```

```{tab-item} MRI

    all_events = layout.get(suffix='events', return_type='filename')
    print(all_events)

    #Output: It will give you all the events, both .tsv and .json files for every participant. It's a very long output.

```
````

The 'get()' function allows you to combine multiple parameters to narrow down your search based on your specific needs.

If your BIDS dataset includes metadata for event files (i.e. a '.json' file describing the columns of your '.tsv' event file), you can specify if you want to search for the metadata or the actual event files by setting the extension parameter to '.json' or '.tsv', respectively.


````{tab-set}
```{tab-item} MEG

    events_sub009_deduc = layout.get(suffix='events', subject='009', extension='.tsv', task='deduction', returntype='filename')
    print(events_sub009_deduc)

    #Output
    #The tsv file of the deduction task of the ninth subject: 
    #['./ancp-bids/test/data/ds003483/sub-009/ses-1/meg/sub-009_ses-1_task-deduction_run-1_events.tsv']

```

```{tab-item} MRI

    events_sub08 = layout.get(suffix='events', sub='08', run='02', extension='.tsv', return_type='filename')
    print(events_sub08)

    #Output
    #The tsv file of the 2nd run of the eigth subject: 
    #['/home/abaxman/.ancp-bids/datasets/ds005/sub-08/func/sub-08_task-mixedgamblestask_run-02_events.tsv']

```
````
