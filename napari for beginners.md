---
jupytext:
  formats: ipynb,md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.10.3
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# napari for beginners

+++

## about napari

napari is a fast, interactive, multi-dimensional image viewer, with [a vibrant plugin ecosystem](https://www.napari-hub.org/) that expands its capability to tackle various domain-specific visualization and analysis needs. It is built on Qt (for the GUI), vispy (for performant GPU-based rendering), and the scientific Python stack (numpy, scipy, and scikit-image). 

napari is an open source project on [GitHub](https://github.com/napari/napari) to facilitate transparency, reuse, and extensibility. 

At its core, it provides critical viewer features out-of-the-box, such as support for large multi-dimensional data; provide “layers” to simultaneously visualize images, models, and analysis results; and easy manual, interactive annotation in 3D. 

+++

## what's covered here

This tutorial is for napari first-timers to give them a quick glance of what napari does, and give it a try right away. We will cover:

- Installation 
- Open an image
- View the image in 2D/3D
- Manually add points to label cells
- Make an animation

Along the way, you will see how to access napari functions from Python code and from GUI - though for different purposes, one method might be easier than another. 

You will also see some examples of plugins. The core napari viewer focuses on domain-agnostic functions i.e.<TO DO>  

** This tutorial uses napari 0.4.13. <br>

+++

### Installation

- For those familiar with Python:

    napari can be installed on most macOS, Linux, and Windows systems with Python 3.7, 3.8, and 3.9 using pip:

```python
pip install 'napari[all]'
```
    Once installed, simply run
    
```python
napari
```

- Or download the bundled app for simple installation:

    [Linux installation](napari-0.4.13-Linux-x86_64.zip)<br>
    [macOS installaion](napari-0.4.13-macOS-x86_64.zip)<br>
    [Windows installation](napari-0.4.13-Windows-x86_64.zip)<br>

    Note: 0.4.13 bundled app is missing sample menu data ([issue 3968](https://github.com/napari/napari/issues/3968))
    
    Note: for the latest release, please visit [here](https://github.com/napari/napari/releases) and look for Assets.

If you run into any issue, please visit the more detailed [installation guide](https://napari.org/tutorials/fundamentals/installation.html), or report an issue on GitHub! 

+++

### Open an image

napari natively supports tiff (and other formats supported by skimage.io.imread) as input image file format.<br>
Try downloading [this ome tiff file](https://downloads.openmicroscopy.org/images/OME-TIFF/2016-06/MitoCheck/00001_01.ome.tiff), and drag and drop the file in napari.

Additional input file formats may be supported [by plugins](https://www.napari-hub.org/). 
Try [napari-aicsimageio](https://www.napari-hub.org/plugins/napari-aicsimageio) if you have czi, lif, or nd2 files.

```{code-cell} ipython3
:tags: [hide-cell]

import napari
viewer = napari.Viewer()
from skimage import data
#load multichannel image in one line, with additional options
viewer = napari.view_image(data.cells3d(), channel_axis=1, name=["membrane", "nuclei"])
viewer.dims.ndisplay = 3
```

````{tabbed} napari in code

```python
import napari
viewer = napari.Viewer()
from skimage import data
#load multichannel image in one line, with additional options
viewer = napari.view_image(data.cells3d(), channel_axis=1, name=["membrane", "nuclei"], colormap=["green", "magenta"])
viewer.dims.ndisplay = 3
```

````

````{tabbed} napari in GUI gif
![SegmentLocal](file_open.gif "segment")
````

+++

## Install plugins

[napari hub](https://www.napari-hub.org/) lets users browse existing napari plugins. Most plugins can be installed either via pip install, or from napari viewer.

````{tabbed} pip install

```python
pip install NicePlugin
```

````

````{tabbed} napari viewer plugin install
place holder for plugin install gif
````

+++

## Get image info

Image dimension <br>
voxel size and time interval <br>

```{code-cell} ipython3
print("image dimension in (z,y,x):", viewer.layers['nuclei'].data.shape)
print("image voxel size for (z,y,x):", viewer.layers['nuclei'].scale)
```

## Adjust image display

Both API and GUI have flexible image display control.<br>

For other display options, see [napari image layer API](https://napari.org/api/stable/napari.layers.Image.html).

+++

````{tabbed} napari in code

```python
#change nuclei color to magenta
viewer.layers['nuclei'].colormap = 'red'
viewer.layers['membrane'].colormap = 'green'
```

````

````{tabbed} napari in GUI gif
![SegmentLocal](colormap.gif "segment")
````

+++

## File saving

Default or recommended file formats for each layer type:
???

````{tabbed} napari in code

```python
napari.save_layers(path, layers)
```

````

````{tabbed} napari in GUI gif
place holder for file saving gif
````

```{code-cell} ipython3
:tags: [hide-cell]

viewer.close()
```
