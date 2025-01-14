# uavsar_pytools

<img src="https://github.com/SnowEx/uavsar_pytools/blob/main/title_figure.png" width="1600">

Python tools to download and convert binary Uavsar images from the Alaska Satellite Facility and Jet Propulsion Laboratory databases. Developed by Zachary Keskinen and Jack Tarricone with guidance from Dr. Hans Peter Marshall of Boise State University, Micah Johnson with m3works, and Micah Sandusky with m3works.

## Installing

We are working to make this package pip installable. To run this repository locally using Jupyter Lab or Notebook:

1. Navigate to where you want the files stored, and clone it to your local machine:

```console
 git clone https://github.com/SnowEx/uavsar_pytools.git
 ```

2. Install the environment. The repository includes an environment.yml that contains a list of all the packages needed to run this tutorial. These lines will also activate your widget extension for the download progress bar. To install them using conda run:

```console
conda env create -f environment.yml
conda activate uavsar_pytools
jupyter nbextension enable --py widgetsnbextension
python -m ipykernel install --user --name=uavsar_pytools
```

3. Start Jupyter:

```console
jupyter-lab
```


## Usage

The fundamental class of uavsar_pytools is the `UavsarScene`. This class is used for downloading, unzipping, and converting binary UAVSAR files into Geotiffs in WGS84. In order to use the class you will need to instantiate an instance of the class to hold your specific url and the image data. Please see the included tutorial and code snippet below. After instantiating the class you can call `scene.url_to_tiffs()` to fully download and convert the Uavsar images into analysis ready tiffs. The two required inputs are a url to an ASF or JPL zip file (if looking to download a single image see `UavsarImage` in the included notebooks) and that has been ground referenced (must have a .grd or \_grd in the name) along with a directory that you want to store the image files in.

```python
from uavsar_pytools.UavsarScene import UavsarScene
zip_url = 'https://datapool.asf.alaska.edu/INTERFEROMETRY_GRD/UA/INTERFEROGRAM_OR_POLSAR_GRD.zip'
image_directory = '~/directory/to/store/images/'
scene = UavsarScene(url = zip_url, work_dir= image_directory) #instantiating an instance of the UavsarScene class.
scene.url_to_tiffs()
```

To get each image's numpy array the class has an `scene.images` property that contains the type, description, and numpy array for each image in the zip file. This is available after running `scene.url_to_tiffs()`.

```python
print(scene.image[0]['type'] # figure out the type of the first image
scene.images[0]['array'] # get the first image numpy array for analysis
```

For quick checks to visualize the data there is also a convenience method `scene.show(i = 1)` that allows you to quickly visualize the first image, or by iterating on i = 2,3,4, etc all the images in the zip file. This method is only available after converting binary images to array with `scene.url_to_tiffs()`.

## Need more help?

The notebook folder in this repository has example notebooks for how to utilize this repository or reach out with questions, features, bugs, or anything else.
