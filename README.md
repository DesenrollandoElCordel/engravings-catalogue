# engravings-catalogue

This repository contains the description of each engraving of the [Moreno corpus](https://github.com/DesenrollandoElCordel/Moreno-TEI-files).

## Workflow
### 1. Extraction of the engravings
The [XML-Page files](https://github.com/DesenrollandoElCordel/Moreno-OCR-files) produced by the OCR tool Transkribus not only give us the coordinates of each line of text, but also the coordinates of the illustrations. These coordinates are encoded with a \<GraphicRegion\> markup.

<img src="Readme-pictures/GraphicRegionMarkup_XmlPage.png" width="700px" />

Each illustration has been extracted with the Python script [extraction_gravures.py](https://github.com/DesenrollandoElCordel/code-python/blob/main/extraction_gravures.py). This script gets the coordinates of each illustration and transforms them into a rectangular zone (x/y + width/height) to ease the extraction and to overcome an issue with the order of the coordinates in the XML Page files.
These new coordinates are recorded in ...

### 2. Description of the illustrations
#### 2.1. General description
The illustrations were first described in an [Excel file](Index_Grabados_Moreno.xlsx). We indicate the identifier of the *pliego* and the number of the page from which the illustration was extracted ; its coordinates on this page ; the title of the pliego, as well as its date, publisher and place of publication ; several keywords spread in different categories ; the list of similar illustrations in the corpus ; and finally some technical information about the status of the data (extracted, encoded, etc.).
#### 2.2. Keywords categories
Specific categories and keywords has been created to fit the particularities of *pliegos*' illustrations.
These categories are described in an XML TEI file ([taxonomy_grabados.xml](taxonomy_grabados.xml)), which follows the [model](https://teipublisher.com/exist/apps/tei-publisher/doc/documentation.xml?odd=docbook.odd&id=facets) recommended by the application [TEI-Publisher](http://teipublisher.com/exist/apps/tei-publisher-home/index.html) that we are using for the publication Web of our project.

<img src="Readme-pictures/Example_Taxonomy_Category.png" width="300px"/>

The xml:id of these categories and keywords are then used in the Excel file to describe each illustration.

<img src="Readme-pictures/Example_Keywords_ExcelFile.png" width="200px"/>

#### 2.3. Detection of similarity
To detect similar illustrations in the Moreno Corpus, we used the [VGG Image Search Engine (VISE)](https://www.robots.ox.ac.uk/~vgg/software/vise/index.html), developed by the Department of Engineering Science of the Oxford University.
The results obtained with this tool have been noted in the Excel file.

<img src="Readme-pictures/Example_SimilarIllustrations_ExcelFile.png" width="300px"/>

### 3. Encoding
The [xml-files folder](xml-files) contains the description of each illustration with a XML TEI file. These files have been generated from the Excel file with the Python script [xslx_tei_files.py](https://github.com/DesenrollandoElCordel/code-python/blob/main/xslx_tei_files.py).
This script transforms each line of the Excel file into a TEI file, which contains the following information :

- The name of the illustration (i.e. its identifier) ;
- The date (`\<date\>`), the publisher (`\<publisher\>`) and the publication place (`\<pubPlace\>`) ;
- The DOI identifier of the overall catalogue (`\<ident type="DOI"\>`)
- Information about the image of the *pliego* (`\<figure\>`) from which the illustrastion was extracted. A `\<graphic>` element contains the name of the image and the coordinates of the illustration. We also add the title of the *pliego* with `\<figDesc\>`.
- Information about similar illustrations (`\<note type="similar_ejemplar"\>`). Each similar illustration is encoded with `\<item\>`. We precise the name of the illustration (`\<title\>`), the date of publication (`\<date\>`) and the title of the *pliego* (`\<locus\>`).
- For developing purposes, we present the keywords in two different ways : `\<catRef\>` for the creation of a faceted search on the Web application and `\<keywords\>` for the presentation of bibliographical metadata.

The ODD and the schema used for the encoding of this catalogue can be found in the Schema folder.
