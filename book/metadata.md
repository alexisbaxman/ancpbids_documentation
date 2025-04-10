
# Querying for metadata
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

