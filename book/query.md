# User Documentation

## Fetch an existing BIDS dataset

ancpBIDS is able to find and load specific files from your PC. With 'fetch_dataset()', even without unzipping your dataaset, ancpBIDS will be able 

succeeds, even if you haven't unzip your dataset, dataset_path will contain the path to it. Also, in your PC folder _'~/.ancp-bids/datasets'_ you will find the zip file (f.e. ds005-testdata.zip) and the content extracted. If you run the code again, it won't create unnecessary copies.


````{tab-set}
```{tab-item} MEG

    from ancpbids import utils
    dataset_path = utils.fetch_dataset('ds005')

```

```{tab-item} MRI

    from ancpbids import utils
    dataset_path = utils.fetch_dataset('ds003483')

```
````


## Creating a Layout
A core functionality of ancpBIDS is to extract information from datasets. Once we fetch the path to our dataset folder, we can use _BIDSLayout_ to create a **map** (layout object) of your dataset, from where you can easily retrieve information.

    from ancpbids.pybids_compat import BIDSLayout
    layout = BIDSLayout(dataset_path)


## Perform some basic queries
With layout held in-memory, we can now use several functions to extract some useful information of the dataset.

* Get all subjects in the dataset

````{tab-set}
```{tab-item} MEG

    subs = layout.get_subjects()
    print(subs)

    # Output: 
    #['009', '012', '013', '014', '015', '016', '017', '018', '019', '020', '021', '022', '023', '024', '025', '026', '027', '028', '029', '030', '031']

```

```{tab-item} MRI

    subs=layout.get_subjects()
    print(subs)

    #Output:
    # ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16']

```
````


* Find how many runs there are:
````{tab-set}
```{tab-item} MEG

    runs=layout.get_runs()
    print(runs)
    #Output
    #['1']

```

```{tab-item} MRI

    sruns=layout.get_runs()
    print(runs)
    #Output:
    #['01', '02', '03']

```
````
Note that the returned runs are collected over all subjects and it is not guaranteed that each participant has the same number of runs.

* Check out the tasks of the experiment
````{tab-set}
```{tab-item} MEG

    tasks = layout.get_tasks()
    print(tasks)

    #Output:
    #['deduction','induction']

```

```{tab-item} MRI

    task = layout.get_task()
    print(task)

    #Output:
    #['mixedgamblestask']

```
````

Subjects, runs and tasks are common entities in BIDS. These simple queries are build in as _'layout.get_NameOfTheEntity()'_. If the entity does not exist in the dataset or is not properly written, the query will return _'[]'_ (empty list). 

If you want to check which entities exist in your dataset, you can use the following function to receive a dictionary with all entities in the dataset and its respective values.


````{tab-set}
```{tab-item} MEG

    avail_entitities=layout.get_entities()
    print("Entities: ", list(avail_entitities.keys()))
    print("Value of task: ", avail_entitities['task'])

    #Output:
    #Entities:  ['sub', 'ses', 'task', 'run', 'desc']
    #Value of task:  {'deduction', 'induction'}

```

```{tab-item} MRI

    avail_entitities=layout.get_entities()
    print("Entities: ", list(avail_entitities.keys()))
    print("Value of task: ", avail_entitities['task'])

    #Output:
    #Entities:  ['task', 'sub', 'run', 'ds', 'type']
    #Value of task:  {'mixedgamblestask'}

```
````

## Querying for metadata
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



## Next section:
In the next section we will continue with more Advanced Queries. 
