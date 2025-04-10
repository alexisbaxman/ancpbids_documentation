# Let's get started with ancpBIDS

## Installation
To install ancpBIDS, run the following command in your terminal:

    pip install ancpbids

It can also be upgraded:

    pip install --upgrade ancpbids


## Download an existing BIDS dataset

ancpBIDS was build for BIDS compatible datasets. Therefore, we offer you to download a test dataset from our [github](https://github.com/ANCPLabOldenburg/ancp-bids-dataset) so you can follow this tutorial. These datasets are only meant to learn how to use ancpBIDS, and are not expected to be used in any kind of research. We offer you two types: a MEG dataset ('ds003483') and a MRI dataset ('ds005'). 
If you have your own BIDS dataset, feel free to use those instead. Do not forget to adapt the code from the user documentation to your specific dataset.

## Virtual environments
Before starting with the tutorial, we want to briefly explain you about virtual environments and containerization.
Virtual environments create isolated and sel-contained workspaces, allowing us to manage project-specific dependencies separatedly from system-wide installation. This isollation has several benefits:
- **Avoid dependency conflicts:** prevents interferences between project-specific and system-wide dependenciesm, such as common erors related to version mismatches.
- **Transparency and Open Science:** Ensures that others can replicate your results and reproduce your analysis reliably.

<img src="../static/environment.jpg" alt="bids-schema" width="600px" align="center">

To create and activate your virtual environment, follow these steps:
1. Navigate to the directory where you want to create the environment using the `cd` command in the terminal.
2. Create the virtual environment:

        python3 -m venv <your_environment_name>

3. Activate the virtual environment:

        source /path/to/environment/bin/activate
