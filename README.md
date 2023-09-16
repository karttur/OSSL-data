# OSSL-data

Example framework structure for running the [ossl-xspectre python package](https://github.com/karttur/OSSL-pydev) for data over Sweden downloaded from the [Open Soil Spectral Library (OSSL)](https://explorer.soilspectroscopy.org). The full manual for downloading and processing data from OSSL using the ossl-xspectre python package together with the example data in this repo, is available at [https://karttur.github.io/soil-spectro/](https://karttur.github.io/soil-spectro/).

## Application

This repo (https://github.com/karttur/OSSL-data) contains processed data over Sweden from OSSL along with the command structure for:

1. Recreating processed data from an OSSL data download,
2. Plotting spectral data, and
3. Machine learning modelling of laboratory determined soil properties from spectral data.

The processed data over Sweden is available in 2 files:

- [/Sweden/LUCAS/arranged-data/visnir/params-visnir_LUCAS_460-1050_10.json](https://github.com/karttur/OSSL-data/tree/main/Sweden/LUCAS/arranged-data/visnir/params-visnir_LUCAS_460-1050_10.json)
- [/Sweden/LUCAS/arranged-data/visnir/data-visnir_LUCAS_460-1050_10.json](https://github.com/karttur/OSSL-data/tree/main/Sweden/LUCAS/arranged-data/visnir/daat-visnir_LUCAS_460-1050_10.json).

### Creating processed data from an OSSL data download

To create processed OSSL ready for plotting and modelling, you need to follow these steps:

1. Clone of download this repo,
2. Download an OSSL dataset from [Open Soil Spectral Library (OSSL)](https://explorer.soilspectroscopy.org),
3. Move the downloaded OSSL data (always named "data.zip") to the folder "/Sweden/LUCAS/data" in the clone/download of this repo,
4. Explode the downloaded zip-file ("data.zip"),
5. Edit the following files:
- /import_ossl.json
- /Sweden/LUCAS/arranged-data/extract_rawdata.txt
- /Sweden/LUCAS/arranged-data/json-import/import_OSSL-LUCAS-SE_nir_460-1050_10.json

The script "OSSL_import.py" requires one parameter, the local path to the file "import_ossl.json". "import_ossl.json" defines the local folder and file paths for the source and target data:

```
{
  "rootpath": "/Local/path/to/OSSL/Sweden/LUCAS",
  "sourcedatafolder": "data",
  "arrangeddatafolder": "arranged-data",
  "jsonfolder": "json-import",
  "projFN": "extract_rawdata.txt",
  "createjsonparams": false
}
```

You only need to change the "rootpath" to reflect the local setup on your machine. The other paths fit the structure of the data in this repo.

When executed the script "OSSL_import.py" will look for a text file:

"rootpath"/"arrangeddatafolder"/"projFN"

With the parameters set as above this becomes the path:

```
/Local/path/to/OSSL/Sweden/LUCAS/arranged-data/extract_rawdata.txt
```

This file is downloaded with this repo, and you need to edit the paths also in that file to reflect your local setup:

```
# OSSL LUCAS Sweden data

/Local/path/to/OSSL/Sweden/LUCAS/arranged-data/json-import/import_OSSL-LUCAS-SE_nir_460-1050_10.json
```

The project file for importing OSSL data in this example links to a single json import command files. You can, however, add any number of input command files, e.g. importing different wavelength regions, bandwidths or source datasets.

Edit the "rootFP" given in each json import command file linked in the project file:

```
"rootFP": "/Local/path/to/OSSL/Sweden/LUCAS",
```

If you now run the script "OSSL_import.py" the processed data over Sweden will be recreated. Following the same steps you can download and process OSSL data over any other region.

### Plotting spectral data

To plot the spectral example data over Sweden from OSSL, you need to follow these steps:

1. Clone of download this repo,
2. Edit the following files:
- /plot_ossl.json
- /Sweden/LUCAS/plot_spectra.txt
- /Sweden/LUCAS/arranged-data/json-plots/plot-OSSL-LUCAS-SE_nir_460-1050_5.json

The script "OSSL_plot.py" requires one parameter, the local path to the file "plot_ossl.json". "plot_ossl.json" defines the local folder and file paths for the source and target data:

```
{
  "rootpath": "/Local/path/to/OSSL/Sweden/LUCAS",
  "sourcedatafolder": "data",
  "arrangeddatafolder": "arranged-data",
  "jsonfolder": "json-plots",
  "projFN": "plot_spectra.txt",
  "createjsonparams": false
}
```

You only need to change the "rootpath" to reflect the local setup on your machine. The other paths fit the structure of the data in this repo.

When executed the script "OSSL_plot.py" will look for a text file:

"rootpath"/"arrangeddatafolder"/"projFN"

With the parameters set as above this becomes the path:

```
/Local/path/to/OSSL/Sweden/LUCAS/arranged-data/plot_spectra.txt
```

This file is downloaded with this repo, and you need to edit the paths also in that file to reflect your local setup:

```
/Local/path/to/OSSL/Sweden/LUCAS/Sweden/LUCAS/arranged-data/json-plots/plot-OSSL-LUCAS-SE_nir_460-1050_5.json
```

The project file for plotting spectral data in this example links to a single json plot command file.

Then you also need to edit the "rootFP" given in each json plot command file linked in the project file:

```
"rootFP": "/Local/path/to/OSSL/Sweden/LUCAS",
```

If you now run the script "OSSL_plot.py" the processed data over Sweden will be plotted on screen and also as saved png files.

### Machine learning modelling

The OSSL data over Sweden contain both spectra and wet laboratory result for a dozen soil properties. You can use the spectral data imported with the script "OSSL_import.py" to model these soil properties from the spectral data. The script for doing that is "OSSL_mlmodel.py". To model the example data over Sweden from OSSL, you need to follow these steps:

1. Clone of download this repo,
2. Edit the following files:
- /ml-model_ossl.json
- /Sweden/LUCASml-model_spectra.txt
- /Sweden/LUCAS/arranged-data/json-ml-modeling/plot-OSSL-LUCAS-SE_nir_460-1050_10.json

The script "OSSL_mlmodel.py" requires one parameter, the local path to the file "model_ossl.json". "model_ossl.json" defines the local folder and file paths for the source and target data:

```
{
  "rootpath": "/Local/path/to/OSSL/Sweden/LUCAS",
  "sourcedatafolder": "data",
  "projFN": "ml-model_spectra.txt",
  "arrangeddatafolder": "arranged-data",
  "jsonpath": "json-ml-modeling",
  "createjsonparams": false
}
```

You only need to change the "rootpath" to reflect the local setup on your machine. The other paths fit the structure of the data in this repo.

When executed the script "OSSL_mlmodel.py" will look for a text file:

"rootpath"/"arrangeddatafolder"/"projFN"

With the parameters set as above this becomes the path:

```
/Local/path/to/OSSL/Sweden/LUCAS/arranged-data/ml-model_spectra.txt
```

This file is downloaded with this repo, and you need to edit the paths also in that file to reflect your local setup:

```
# OSSL LUCAS Sweden machine learning modeling

Local/path/to/OSSL/OSSL/Sweden/LUCAS/arranged-data/json-ml-modeling/model-OSSL-LUCAS-SE_nir_460-1050_10.json
```

The project file for modelling soil properties from spectral data in this example links to a single json model command file.

Then you also need to edit the "rootFP" given in each json model command file linked in the project file:

```
"rootFP": "/Local/path/to/OSSL/Sweden/LUCAS",
```

If you now run the script "OSSL_mlmodel.py" the processed data over Sweden will be modelled, plotted on screen and saved as json files, preserved model setting ("pickle") files and as png images.
