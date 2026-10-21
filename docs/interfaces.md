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

The __Appearance__ tab is always available, and it allows altering RNA backbone and bond color, size of the bases (circles and font), and base index font size. The __General__ tab is also always available, and controls whether non-standard characters are accepted in sequences.

When reactivity data is loaded, an additional __Reactivity__ tab will appear:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_settings_reactivity.png" width="50%"/>
</p>

Through this tab, the user can define the color scale used to render base reactivities. The default scheme uses a simple discretization of values between 0 and 0.3 (low reactivity), 0.3 and 0.7 (medium reactivity) and 0.7+ (high reactivity). Additional stops can be added as needed, or a continuous color scale can be adopted instead.

Similarly, when base-pair/helix annotations are loaded, an additional __Annotations__ tab will appear:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_settings_annotations.png" width="50%"/>
</p>

When outline mode is active, an additional __Outline__ tab appears (see [Outline mode](#outline-mode) below).

Furthermore, several toggles are available in the toolbar to turn on/off the rendering of base indices, reactivities, base-pair/helix annotations and pseudoknots, and, for Stockholm alignments, of inset panels (__I__), annotation labels (__L__), single-stranded 5'/3' ends (__SS__), sequence weighting (the weight icon) and % canonical pairs coloring (__%__). The remaining buttons switch the layout algorithm (NAView/Radiate), toggle the automatic refit upon helix rotation, switch to [outline mode](#outline-mode), open the alignment view, and move the toolbar.


### Outline mode

The __Outline__ toggle reduces the structure to its backbone, drawn as a single thick line: bases, bonds, labels, annotations, legends and inset panels are all hidden. This view is meant for depicting the domain organization of an RNA: any stretch of the backbone can be highlighted in a color of choice, and the result can be exported as SVG.

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_outline_mode.png" />
</p>

Domains can be defined in two ways:

- __By clicking on the backbone.__ Hovering the line shows a marker on the closest base, together with its index (and the index of its pairing partner, e.g. `150 ↔ 193`). A first click sets the start of the domain, a second click its end, in either order. While picking the end, the domain is previewed under the mouse. The color of the next domain can be chosen from the picker in the small bar at the top left of the canvas (each new domain gets a new color by default), __Esc__ cancels a pending start, and __Undo__ removes the last domain.
- __From the Settings dialog.__ The __Outline__ tab lists every domain (name, start base, end base and color) and allows editing them, removing them (__−__), or adding new ones (__+ Add domain__). New domains are named `Domain #1`, `Domain #2`, etc., are black by default, and extend from the end of the previous domain to the end of the RNA. An end position larger than the length of the RNA is automatically set to the last base, and swapped positions are reordered. The tab also controls the thickness of the line.

Domains made by clicking appear in the same list and can be edited there. Positions follow the numbering shown by the index labels (alignment columns for Stockholm alignments), so they are unaffected by the SS ends toggle. A legend with a color box and the name of each domain is shown in the upper right corner of the canvas.

Helices can still be rotated by dragging any paired base, panning and zooming work as usual, and switching structures keeps a separate set of domains for each structure. Turning outline mode off restores the normal visualization. The domains are kept, and are shown again when outline mode is turned back on. __Save SVG__ in outline mode exports the outline, the colored domains and their legend.


### Visualization of structures from Stockholm alignments

Stockholm alignments can be directly rendered by RFview, provided that the `#=GC SS_cons` is present in the alignment.

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_stockholm.png" width="100%"/>
</p>

Rendering faithfully reproduces [Zasha Weinberg's __R2R__](https://sourceforge.net/projects/weinberg-r2r/) as it is run by [R-scape](https://github.com/EddyRivasLab/R-scape) (`r2r --GSC-weighted-consensus`): the same preprocessing, the same sequence weighting and the same per-column rules, so the consensus drawn by RFview matches the one in R-scape's R2R output.

Before the consensus is computed, alignment columns in which fewer than 25% of the sequences have a residue are removed, base pairs losing one of their columns are opened, degenerate nucleotides are treated as unknown and `T`s are converted to `U`s (as R-scape does before calling R2R). Sequences are then weighted, and each remaining column is rendered according to the first matching rule:

Weighted frequency in the column | Rendered as
---------: | :------------
Single nucleotide &ge; 97% / 90% / 75% | That nucleotide, colored in __red__ / __black__ / __grey__
Purines (A+G) or pyrimidines (C+U) &ge; 97% / 90% / 75% | __R__ or __Y__, colored in __red__ / __black__ / __grey__
Any nucleotide present &ge; 97% / 90% / 75% / 50% | Filled __red__ / __black__ / __grey__ / __white__ circle
None of the above | Column not rendered, unless it is base-paired (paired columns are always kept, as an empty circle)

Gaps count towards the column total. Hovering a base shows the (weighted) percentage of each nucleotide in that column.

__Sequence weighting.__ R2R's Gerstein-Sonnhammer-Chothia (GSC) tree weights are used for alignments of up to 1,000 sequences. Above that, position-based (Henikoff) weights are used instead, as GSC becomes too slow in a browser. In both cases every sequence of the alignment contributes to the consensus. The weighting can be turned off with the toolbar toggle (weight icon), in which case raw nucleotide frequencies are shown. Hovering the toggle tells which weighting scheme is in use.

Single-stranded 5&prime;/3&prime; ends are hidden by default, and the __SS__ toggle shows them.

The user can switch between __Structure view__ and __Alignment view__ (available for alignments of up to 5,000 columns). In alignment view, the Stockholm alignment is displayed with alignment columns colored according to the parent helix. The first 1,000 sequences of the alignment are shown:

<p align="center">
  <img src="http://rfview.incarnatolab.com/images/RFview_alignment_view.png" />
</p>

Furthermore, RFview automatically computes the (weighted) percentage of sequences with a canonical base-pair (AU, GC, GU) at each paired position. When a Stockholm structure is loaded, a % canonical pairs toggle button (%) appears in the toolbar. Activating it colors every base-pair using a red→yellow→green gradient. The gradient stop colors are adjustable via the Settings dialog. The same statistic drives the rendering of bonds in the consensus structure: positions where canonical pairs are the majority (&gt;50%) are drawn as a line, while non-canonical-majority positions are drawn as a dot.

Any additional `#=GC SS_cons_*` line in the alignment (pseudoknots, non-canonical interactions, R-scape's CaCoFold motifs, ...) is labeled on the structure, and its base pairs are shown in inset panels at the top left of the canvas, one panel per annotation name (plus one per pseudoknot of the main `SS_cons`). Hovering an inset panel highlights the corresponding bases in the structure. Inset panels and labels can be hidden with the __I__ and __L__ toggles.


## Command Line Interface (CLI)

When packed as a standalone Electron app, RFview can be invoked from command line to directly generate structure plots in SVG format. Stockholm alignments are streamed, so there is no limit on their size, and the consensus is computed from every sequence, exactly as in the GUI.

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
__--percCanonical__ | | For Stockholm alignments, colors every base-pair by % canonical pairs computed from the alignment
__--helixCovAnno__ | string | R-scape's .helixcov helix-level covariation file
__--layout__ | string | Layout for RNA secondary structure rendering:  __auto__ (automatically determines the best layout between naview and radiate to avoid overlaps between helices), __naview__, or __radiate__ (Default: __auto__)
__--svg__ | string | Path to the output SVG file (Default: __&lt;structureFile basename&gt;.svg__)
__--pdf__ | string | Path to the output PDF file
__--noLegend__ | | Omits legends from the exported SVG
__--noPk__ | | Omits pseudoknot archs from the exported SVG<br/>__Note:__ this has no effect on Stockholm alignments (use `--noLabels` and `--noInsets` instead)
__--noLabels__ | | Omits Stockholm annotation labels (`SS_cons` lines) from the exported SVG
__--noInsets__ | | Omits inset panels for non-nested interactions in Stockholm alignments from the exported SVG
__--incSsEnds__ | | Includes single-stranded 5'/3' ends in Stockholm structures
