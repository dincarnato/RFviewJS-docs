# Interfaces

## Graphical User Interface (GUI)

The main RFviewJS/RFview GUI consists of a toolbar and a canvas area:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_GUI.gif" border="1"/>
</p>

The toolbar contains the following:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_toolbar.png" width="50%"/>
</p>


### Loading structures, reactivity data &amp; annotations

Structures can be loaded in one of four ways:

- Structure files via the __Load structure/reactivity/annotation__ dialog
- Structure files by direct drag-and-drop onto the canvas area
- Fetching of alignments from __[Rfam](https://rfam.org/)__
- Manual sequence/structure input via the __Manually enter sequence &amp; structure__ dialog

The __Load structure/reactivity/annotation__ dialog provides an easy and intuitive interface for data loading, enabling the simultaneous import of structures, reactivity data and annotations:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_load_data.png" width="50%"/>
</p>

Multiple files (structure, reactivity, annotations) can be simultaneously loaded, and they are displayed as lists the user can positionally match:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_load_data_rearrange.png" width="50%"/>
</p>

In the above example, a dot-bracket file containing 2 structures was imported, along with 2 XML reactivity files. The used can use the arrows to rearrange the files, such that the first structure will get the reactivities from the first XML file, the second structure from the second XML file, and so on.

The same dialog will pop-up if the user attempts to load reactivities on top of previously loaded structures. RFview will only display in the list the structures whose sequence matches the one in the XML file. If multiple structures match the sequence of an XML file, the user can remove the unwanted structure files from the list by clicking on the __&times;__.

Alternatively, the __Manually enter sequence &amp; structure__ dialog allows the user to directly type in a structure and a sequence to be loaded. If no sequence is provided, bases will be displayed as Ns:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_manual_input.png" width="50%"/>
</p>


### Customizing structure rendering settings

Upon loading, diplay settings can be adjusted through the __Settings__ dialog. Multiple settings tab will be present, depedending on whether a reactivity and/or an annotation file has been loaded for the current structure:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_settings.png" width="50%"/>
</p>

The __Apparance__ tab is always available, and it allows altering RNA backbone and bond color, size of the bases (circles and font), and base index font size.

When reactivity data is loaded, an additional __Reactivity__ tab will appear:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_settings_reactivity.png" width="50%"/>
</p>

Through this tab, the user can define the color scale used to render base reactivities. The default scheme uses a simple discretization of values between 0 and 0.3 (low reactivity), 0.3 and 0.7 (medium reactivity) and 0.7+ (high reactivity). Additional stops can be added as needed, or a continuous color scale can be adopted instead.

Similarly, when base-pair/helix annotations are loaded, an additional __Annotations__ tab will appear:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_settings_annotations.png" width="50%"/>
</p>

Furthermore, several of toggles are available in the toolbar to turn on/off the rendering of base indices, reactivities, base-pair/helix annotations and pseudoknots.


### Visualization of structures from Stockholm alignments

Stockholm alignments can be directly rendered by RFview, provided that the `#=GC SS_cons` is present in the alignment.

Rendering mostly follows the same rules as [Zasha Weinberg's __R2R__](https://sourceforge.net/projects/weinberg-r2r/) algorithm, with minor improvements:

Base       | Rendered as
---------: | :------------
Single nucleotide present &ge; 97% | That nucleotide, colored in __red__
Single nucleotide present &ge; 90% | That nucleotide, colored in __black__
Single nucleotide present &ge; 75% | That nucleotide, colored in __grey__
Two or three nucleotides, each present &ge; 30%, combined &ge; 75% | IUPAC code, colored according to the same thresholds used for single nucleotides
Any nucleotide present &ge; 97% | Filled __red__ circle
Any nucleotide present &ge; 90% | Filled __black__ circle
Any nucleotide present &ge; 75% | Filled __grey__ circle
Any nucleotide present &ge; 50% | Filled __white__ circle
None of the above | Alignment column not rendered

The user can switch between __Structure view__ and __Alignment view__. In alignment view, the Stockholm alignment is displayed with alignment columns colored according to the parent helix:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_alignment_view.png" />
</p>


## Command Line Interface (CLI)

When packed as a standalone Electron app, RFview can be invoked from command line to directly generate structure plots in SVG format.

### Usage

```bash
$ RFview --structureFile structure.db
$ RFview --structureFile structure.db --xml reactivity.xml --svg plot.svg
$ RFview --structureFile alignment.sto --basePairAnno alignment.cov --layout naview --svg plot.svg
```

To list all avalailable parameters, simply type:

```bash
$ RFview --help
```

Parameter         | Type | Description
----------------: | :--: |:------------
__--structureFile__ | string | Path to a structure file (.db, .dbn, .ct, .txt) or to a Stockholm alignment [required]
__--rfam__ | string | Rfam family ID to fetch directly from Rfam (e.g., RF00162)<br/>__Note:__ `--rfam` and `--structureFile` are mutually exclusive
__--xml__ | string | Reactivity file (in [RNA Framework's XML format](https://rnaframework-docs.readthedocs.io/en/latest/rf-norm/#output-xml-files))
__--basePairAnno__ | string | Pair-annotation file (.tsv, .txt) or R-scape's .cov file
__--helixCovAnno__ | string | R-scape's .helixcov helix-level covariation file
__--layout__ | string | Layout for RNA secondary structure rendering:  __auto__ (automatically determines the best layout between naview and radiate to avoid overlaps between helices), __naview__, or __radiate__ (Default: __auto__)
__--svg__ | string | Path to the output SVG file (Default: __&lt;structureFile basename&gt;.svg__)
__--noLegend__ | | Omits legends from the exported SVG
__--noPk__ | | Omits pseudoknot archs from the exported SVG<br/>__Note:__ this has no effect on Stockholm alignments (use `--noLabels` and `--noInsets` instead)
__--noLabels__ | | Omits Stockholm annotation labels (`SS_cons` lines) from the exported SVG
__--noInsets__ | | Omits inset panels for non-nested interactions in Stockholm alignments from the exported SVG

