# API Reference

__RFviewJS__ is a self-contained JavaScript module for RNA secondary structure visualization and editing. It requires no build step and no external dependencies: a single `<script>` tag is enough.


## Installation

To install __RFviewJS__ on your webpage, just obtain `RFview.js` from the [Git repository](https://github.com/dincarnato/rfviewjs) (under `scripts/RFview.js`), upload it to your webserver and include it with a plain `<script>` tag:

```html
<script src="path/to/RFview.js"></script>
```

Alternatively, you can directly import it from the official RFviewJS website:

```html
<script src="https://rfview.incarnatolab.com/scripts/RFview.js"></script>
```

The module exports a single global class, `RFviewJS`. 


## Quick start

```html
<!DOCTYPE html>
<html>
<head>
  <script src="RFview.js"></script>
  <style>
    html, body { height: 100%; margin: 0; }
    #viewer { width: 100%; height: 100%; }
  </style>
</head>
<body>
  <div id="viewer"></div>
  <script>
    const viewer = new RFviewJS(document.getElementById('viewer'));

    viewer.load({
      sequence:  'GGGUCUAUCUAUUGGAGAGAACCAUGGAGAAACCC',
      structure: '((((...(((((.((......)))))))...))))',
    });
  </script>
</body>
</html>
```

Several usage examples are available from the [Git repository](https://github.com/dincarnato/rfviewjs) (under `examples/`).


## Constructor

```js
const viewer = new RFviewJS(container, options);
```

`container` is any DOM element. The viewer fills it completely, so give the element explicit dimensions (usually via CSS).

### Viewer options

| Option | Type | Default | Description |
|---|---|---|---|
| `toolbarPosition` | `'left'` \| `'right'` \| `'top'` \| `'bottom'` | `'left'` | Toolbar's positioning in the canvas |
| `statusBar` | `boolean` | `true` | Shows the bottom status bar containing general information about the structure (sequence length, base-pair count, etc.) |
| `canvasDrop` | `boolean` | `true` | Enables loading of structure/reactivity/annotation files via direct drag-and-drop onto the canvas |
| `layout` | `'auto'` \| `'radiate'` \| `'naview'` | `'auto'` | RNA secondary structure rendering algorithm. `'auto'` computes both NAView and Radiate layouts, counts the number of helix crossings in each, and picks the one with fewer crossings. NAView wins when its count is &lt; Radiate's (within tolerance, see `autoLayoutTolerance` below) |
| `autoLayoutTolerance` | `numeric` | `0` | Maximum number of helix crossings that can be allowed to still prefer Radiate layout over NAView |
| `showIndices` | `boolean` | `true` | Shows position index labels |
| `showColors` | `boolean` | `true` | Shows reactivity colors to bases on load (see `colorMap` below) |
| `showPairAnnotations` | `boolean` | `true` | Shows base-pair/helix-level annotation boxes on load |
| `showInsets` | `boolean` | `true` | Shows inset panels of non-nested interactions for Stockholm structures on load |
| `showLabels` | `boolean` | `true` | Shows labels of SS_cons annotations for Stockholm structures on load |
| `showSsEnds` | `boolean` | `false` | Shows single-stranded (unstructured) nucleotides at either ends of a structure (off by default) |
| `transitionDuration` | `numeric` | `600` | Duration (in ms) of the transition when switching between alternative structures that share the same sequence |
| `buttons` | `object` \| `false` | all on | Fine-grained toolbar control (see [Toolbar buttonw](#toolbar-buttons) below) |
| `width` | `numeric` \| `string` | — | Width of the container (e.g. `800` or `'100%'`) |
| `height` | `numeric` \| `string` | — | Height of the container |
| `id` | `string` | — | Used as the basename when saving the structure as SVG |
| `colorMap` | `object` | — | A [colorMap object](#color-maps) used as the default for the initial `load()` call triggered by the constructor (__Note:__ it has no effect on subsequent `load()` calls) |
| `relaxedSequence` | `boolean` | `false` | Disables sequence character validation, allowing any character (custom alphabets) to be used. When enabled, all base pairs are rendered as single lines regardless of the base identity |

The constructor always calls `load(options)` at the end, so any key accepted by `load()` can be passed directly to the constructor.


### Toolbar buttons

The module allows full toolbar customization. Toggling of individual buttons can be controlled as it follows:

```js
const viewer = new RFviewJS(container, {
  buttons: {
    upload:          true,   // Structure/Reactivity/Annotation file upload
    rfam:            true,   // Fetch alignment from Rfam
    manualInput:     true,   // Manual input of sequence & structure
    cleanOne:        true,   // Clear current structure
    cleanAll:        true,   // Clear all structures
    zoomIn:          true,   // Zoom in
    zoomOut:         true,   // Zoom out
    fit:             true,   // Fit structure to canvas
    reset:           true,   // Layout reset
    save:            true,   // SVG export
    indices:         true,   // Toggle display position indices
    colorMap:        true,   // Toggle display reactivities
    pairAnnotations: true,   // Toggle display base-pair/helix-level annotations
    pseudoknots:     true,   // Toggle display pseudoknots
    insets:          true,   // Toggle display of inset panels (Stockholm structures)
    labels:          true,   // Toggle display of labels from SS_cons annotation lines (Stockholm structures)
    ssEnds:          true,   // Toggle display single-stranded bases at either ends of a structure (when present)
    layout:          true,   // Structure rendering layout switching
    toolbarPos:      true,   // Toolbar repositioning
  }
});
```

Omitted keys default to `true`. Setting `buttons: false` is equivalent to setting every key to `false`. Please note, __the Settings and About buttons cannot be hidden__.


## Public methods

| Method | Argument(s) | Description |
|---|---|---|
| `fit()` | | Fits the current structure to the canvas, with a small padding. Called automatically after every `load()` |
| `reset()` | | Redraws the current structure from scratch (discards any manual helix rotations) |
| `clear()` | | Removes all structures and annotations and resets the viewer to a blank state |
| `clearCurrent()` | | Removes only the currently active structure. The remaining structures stay loaded and the viewer switches to the next one. Falls back to `clear()` if only one structure is loaded |
| `switchToStructure()` | `index` \| `label` | Switches to another structure. Structures can be specified via their 0-based index (which follows the order of loading) or by label string. If sequences match, therefore structures represent alternative conformations of the same RNA, a smooth animated transition is triggered |
| `setShowIndices()` | `bool` | Shows or hides position index labels |
| `setShowColors()` | `bool` | Toggles reactivity coloring |
| `setShowPairAnnotations()` | `bool` | Toggles base-pair/helix-level annotation boxes |
| `setShowInsets()` | `bool` | Toggles inset panels for non-nested interactions (Stockholm structures) |
| `setShowLabels()` | `bool` | Toggles labels for SS_cons annotation lines (Stockholm structures) |
| `setShowSsEnds()` | `bool` | Toggles rendering of single-stranded nucleotides at either ends of a structure |
| `setLayoutAlgorithm()` | `algorithm` | Switches the RNA structure rendering algorithm (`'auto'`, `'radiate'`, or `'naview'`) and re-renders |
| `fetchRfam()` | `id` | Fetches a Stockholm alignment from Rfam by family ID (e.g., `'RF00162'`) and loads it |
| `exportSVGString()` | | Renders the current structure and returns it as an SVG string. Useful for programmatic export without triggering a file-save dialog |


### load()

`load(config)` is the main method. Every key is optional unless stated otherwise.

#### Loading single structures

```js
viewer.load({
  sequence:  'GGGGAUUCCCC',    // Required (Ts are auto-converted to Us)
  structure: '((((...))))',    // Required
  label:     'RNA#1',          // Structure ID/label

  values:     [...],           // Array of per-base reactivities
  showColors: true,            // Whether to apply reactivity coloring on load()
  colorMap:   { ... },         // see "Color maps" section below (can be omitted for default reactivity coloring)
  nanColor:  '#999999',        // Color of bases with NaN values

  pairAnnotations:  [...],     // see "Base-pair annotations" section below
  pairAnnotColorMap: { ... },  // Color map for base-pair annotation boxes
  
  helixAnnotations:  [...],    // see "Helix-level annotations"
});
```

`structure` accepts standard dot-bracket notation. Square brackets `[]`, curly braces `{}`, and angle brackets `<>`, as well as upper-case/lower-case pairs (e.g., `Aa`) are also accepted.

`values` must have the same length as `sequence`. `NaN` can be used for positions with no data, which will be colored by `nanColor`.


#### Multiple structures in one canvas

Multiple structures can be simultaneously loaded by passing a `structures` array. Each entry is a structure-level config object. Keys declared at the top level act as shared defaults, and each structure entry can override them individually.

```js
viewer.load({
  sequence:   'GGGAAAUUUCCC',    // Shared sequence
  showColors: true,              // Shared color map display flag
  structures: [
    {
      label:     'Structure 1 — Default reactivity colorMap',
      structure: '(((......)))',
      values:    [ ... ],
      // no colorMap defined, falls back to built-in default
    },
    {
      label:     'Structure 2 — Custom colorMap',
      structure: '(((...)))...',
      values:    [ ... ],
      colorMap:  { ... },
      nanColor:  '#999999',
    },
  ],
});
```

The viewer will automatically display a structure switcher when more than one structure is loaded. Switching between structures with the same sequence triggers a smooth animated transition.

Each entry in `structures` can contain: `label`, `sequence`, `structure`, `values`, `colorMap`, `pairAnnotations`, `pairAnnotColorMap` and `helixAnnotations`.


#### Loading from text: dot-bracket, CT and Stockholm

Raw dot-bracket, CT and Stockholm file contents can be directly passed as `fileText` (or the Stockholm-specific alias `stockholmText`) to the constructor, or to the `load()` method. The format is auto-detected.

```js
// Stockholm alignment
viewer.load({ stockholmText: stockholmFileText, label: 'RF00162' });

// Dot-bracket / CT
viewer.load({ fileText: structureFileText });
```

When `label` is provided, it overrides the name extracted from the file (e.g., `#=GF AC` or `#=GF ID` for Stockholm files). If the file contains multiple records, the label is suffixed with `(1)`, `(2)`, and so on.

Stockholm files are parsed into a consensus structure. The alignment view (conservation colors, alignment track) is shown alongside the structure diagram. Gap-only columns are filtered out. Position labels are remapped so that covariation data loaded afterwards aligns correctly. For additional details, please see __[Visualization of structures from Stockholm alignments](https://rfviewjs-docs.readthedocs.io/en/latest/interfaces/#visualization-of-structures-from-stockholm-alignments)__.

Furthermore, any additional `#=GC SS_cons_*` entry in the file is processed and labeled on the consensus structure. Non-nested interactions (such as pseudoknots, cross-covariations, etc.) are displayed as separate insets and labeled. Hovering on the inset causes the corresponding bases in the consensus structure to glow up.


#### Fetching from Rfam

Alignments can also be directly fetched from __[Rfam](https://rfam.org/)__, by passing an Rfam ID to `rfamId` directly to the constructor, or to the `load()` method:

```js
viewer.load({ rfamId: 'RF00162' });
```

Alternatively, alignments can be fetched via the `fetchRfam()` method after construction:

```js
viewer.fetchRfam('RF00162');
```


#### Multiple Stockholm alignments in one canvas

To load multiple Stockholm files into the same canvas as switchable structures, use `RFviewJS.parseStockholmFile()` to pre-parse each file into the structures array format, then spread them into a single `structures` array:

```js
viewer.load({
  structures: [
    ...RFviewJS.parseStockholmFile(stockholmText1, 'RF00162'),
    ...RFviewJS.parseStockholmFile(stockholmText2, 'RF00504'),
  ],
});
```

After loading, covariation data for each alignment must be applied while that structure is active (see [`switchToStructure()`](#public-methods) and [`loadCov()`](#loadcov)):

```js
viewer.switchToStructure(1);      // Switches to structure RF00504
viewer.loadCov(covFileText);      // Loads base-pair covariation data from R-scape's .cov file text
viewer.loadCov(helixCovFileText); // Loads helix-level covariation data from R-scape's .helixcov file text
```


## Color maps

A color map controls how `values` are mapped to base colors. If no `colorMap` is provided, coloring falls back to the built-in reactivity discrete color map:

| Value range | Color | 
|-------------|-------|
| 0-0.3 | `#1f2328` (black) |
| 0.3-0.7 | `#f5c518` (yellow) |
| 0.7+ | `#cc0000` (red) |
| NaN | `#808080` (grey) |


### Shorthand gradient

As a quick shortcut, a two-stop gradient can be created without writing a full colorMap object:

```js
viewer.load({
  sequence:         '...', 
  structure:        '...', 
  values:           [ ... ],
  colorMapMin:      0,          // Minimum value (default: 0)
  colorMapMax:      1,          // Maximum value (default: 1)
  colorMapMinColor: '#4870c8',  // colorMapMin color
  colorMapMaxColor: '#bd0530',  // colorMapMax color
  colorMapNaN:      '#808080',  // Color for NaN positions
});
```


### Full colormap object

For complete control, a full `colorMap` object can be created:

```js
const COLOR_MAP = {
  type:     'discrete',   // 'discrete' or 'gradient'
  min:      0,            // Lower bound for the first stop (gradient only)
  nanColor: '#999999',    // Color for NaN / missing values

  stops: [
    { value: 0.3, color: '#1e3a55' },   // Upper bound of the first stop
    { value: 0.7, color: '#60a5fa' },
    { value: 1.0, color: '#9353ea' },
  ],
};

viewer.load({
  sequence:   '...', 
  structure:  '...', 
  values:     [ ... ],
  showColors: true,
  colorMap:   COLOR_MAP,
});
```

With `type: 'discrete'`, each stop defines the upper bound of a color band. Any value &le; `stops[0].value` will get `stops[0].color`, while values beyond the last stop get the last stop's color.

With `type: 'gradient'`, colors are interpolated linearly between stops. Values below the first stop or above the last stop are clamped.

Stops are sorted by `value` automatically.


## Base-pair annotations

`pairAnnotations` are drawn as colored boxes surrounding specific base-pairs, and they are useful for highlighting, for example, significantly covarying pairs.

Each annotation is an object:

```js
viewer.load({
  sequence, structure,
  pairAnnotations: [
    { i: 5,  color: '#e74c3c' },             // Annotates pair at position 5
    { i: 12, j: 40, color: '#3498db', opacity: 0.5 },
    { i: 20, value: 0.8 },                   // Colored via pairAnnotColorMap
  ],
  pairAnnotColorMap: {
    type: 'gradient',
    stops: [
      { value: 0.0, color: '#ffffff' },
      { value: 1.0, color: '#e74c3c' },
    ],
  },
});
```

where:

| Key | Type | Default | Description |
|---|---|---|---|
| `i` | `numeric` | | 0-indexed position of the first base of the pair (required) |
| `j` | `numeric` | `pairs[i]` | 0-indexed position of the second base of the pair (optional). Defaults to the pair partner of `i` in the current structure |
| `color` | `string` | | Hex color (__Note:__`color` and `value` are mutually exclusive) |
| `value` | `numeric` | | Mapped to a color through `pairAnnotColorMap` (__Note:__`color` and `value` are mutually exclusive) |
| `opacity` | `numeric` | `0.5` | Fill opacity |
| `strokeWidth` | `numeric` | `1.5` | Border thickness |
| `padding` | `numeric` | `5` | Extra padding around the base-pair in scene units |

`i` and `j` must refer to an actual base pair in the structure. The viewer validates annotations at load time and reports any that reference unpaired or out-of-range positions.

__Note:__ when annotating structures loaded from Stockholm alignments, `i` and `j` refer to the original alignment column (0-based), not the rendered position. The viewer remaps it automatically.


## Helix-level annotations

`helixAnnotations` are drawn as colored bounding boxes around entire helices, and they are useful for highlighting, for example, significantly covarying helices.

Each annotation is an object with `i` specifying any paired position within the target helix. The viewer automatically walks outward to find the outermost pair of the helix, then inward to collect all stacked pairs, so the box encompasses the full helix regardless of which position `i` points to.

```js
viewer.load({
  sequence, structure,
  helixAnnotations: [
    { i: 5,  color: '#e74c3c' },
    { i: 20, color: '#3498db', opacity: 0.12, strokeWidth: 2 },
    { i: 40, padding: 30 },
  ],
});
```

where:

| Key | Type | Default | Description |
|---|---|---|---|
| `i` | `numeric` | | 0-indexed position of any base within the target helix (required). Must be a paired position |
| `color` | `string` | `--rv-helix-annot-color` | Hex color of the annotation box. Falls back to the CSS custom property `--rv-helix-annot-color` |
| `opacity` | `numeric` | `0.5` | Fill opacity |
| `strokeWidth` | `numeric` | `1.5` | Border thickness |
| `padding` | `numeric` | `--rv-helix-annot-padding` | Extra padding around the helix in scene units. Falls back to the CSS custom property `--rv-helix-annot-padding` |

__Note #1:__ `helixAnnotations` does not support `value`/`helixAnnotColorMap`. Use `color` directly for per-annotation coloring.

__Note #2:__ when annotating structures loaded from Stockholm alignments, `i` refers to the original alignment column (0-based), not the rendered position. The viewer remaps it automatically.


## Post-load annotation methods

### loadCov()

Loads __[R-scape](https://github.com/EddyRivasLab/R-scape)__'s covariation files (`.cov` or `.helixcov` format), or TSV files (please see __[File formats](https://rfviewjs-docs.readthedocs.io/en/latest/file-formats/#base-pair-helix-level-annotations)__ for more information) onto the currently displayed structure. The method auto-detects the format.

```js
try {
  viewer.loadCov(covFileText);
} catch (e) {
  console.warn('Covariation error:', e.message);
}
```

Base-pair annotations from a `.cov` file are color-coded by E-value, while TSV annotations are colored by group ID (third field). A `.helixcov` file draws a bounding box around each significantly covarying helix.

`loadCov()` throws an exception if the file contains pairs that cannot be mapped onto the current structure (e.g. if the structure was not yet loaded, or if the file belongs to a different alignment). Exceptions can be caught via wrapping in `try/catch`.

When working with multiple structures, `switchToStructure()` can be called first to select the correct target structure before calling `loadCov()`:

```js
viewer.switchToStructure(0);
viewer.loadCov(cov1);

viewer.switchToStructure(1);
viewer.loadCov(cov2);

viewer.switchToStructure(0);   // Goes back to the first structure
```


### loadHelixCov()

Loads a `.helixcov` file directly (bypassing the auto-detect in `loadCov()`). Only significant helices are drawn. Behaviour and error handling are identical to those of `loadCov()`.

```js
viewer.loadHelixCov(helixCovText);
```


## Static methods

| Method | Description |
|--------|-------------|
| `RFviewJS.parseStockholmFile(text, labelFallback)` | Parses a Stockholm alignment and returns an array of structure-record objects suitable for spreading into a `structures` array (the label is taken from `#=GF ID` or `#=GF AC`, falling back to `labelFallback`) |
| `RFviewJS.parseDbFile(text, label)` | Parses a dot-bracket or CT file and returns an array of structure records |
| `RFviewJS.parseCTFile(text)` | Parses a CT file and returns structure records |
| `RFviewJS.parseXmlReactivity(text)` | Parses an RNA Framework XML reactivity file |
| `RFviewJS.parsePairAnnotFile(text)` | Parses a TSV pair-annotation file |
| `RFviewJS.parseCovFile(text)` | Parses an R-scape `.cov` file |
| `RFviewJS.parseHelixCovFile(text)` | Parses an R-scape `.helixcov` file |
| `RFviewJS.buildAnnotColorMap(pairs)` | Builds a color map for a set of pair annotations |


## CSS custom properties

All visual properties are exposed as CSS custom properties set on the `.rv` root element, so any theme can be applied from a stylesheet without touching the JS.


### Color palette

| Property | Default | Description |
|---|---|---|
| `--rv-bg` | `#ffffff` | Canvas and toolbar background |
| `--rv-surface` | `#f6f8fa` | Panel and dialog background |
| `--rv-border` | `#d0d7de` | Border color for panels and controls |
| `--rv-text` | `#1f2328` | Primary text color |
| `--rv-muted` | `#656d76` | Secondary / label text color |
| `--rv-accent` | `#0969da` | Buttons, links, and highlights |
| `--rv-accent2` | `#2da44e` | Secondary accent (green), used for pair formation highlights |
| `--rv-accent3` | `#8250df` | Tertiary accent (purple) |
| `--rv-error-border` | — | Border color for error states |
| `--rv-error` | `#cf222e` | Error messages |


### Structure drawing

| Property | Default | Description |
|---|---|---|
| `--rv-backbone` | `#1f2328` | Backbone line color |
| `--rv-backbone-width` | `2` | Backbone stroke width |
| `--rv-basepair` | `#1f2328` | Base-pair line color |
| `--rv-basepair-width` | `2.2` | Base-pair stroke width |
| `--rv-pseudopair` | `#0969da` | Pseudoknot color |
| `--rv-pseudopair-width` | `2` | Pseudoknot stroke width |
| `--rv-base-fill` | `#eaeef2` | Default (no-data) base circle fill |
| `--rv-base-stroke` | `#1f2328` | Base circle border color |
| `--rv-base-stroke-width` | `2` | Base circle border width |
| `--rv-base-hover` | `#bbd4f0` | Base fill on hover |
| `--rv-base-radius` | `11` | Base circle radius in SVG units |
| `--rv-base-label-color` | `#1f2328` | Nucleotide letter color |
| `--rv-base-label-font` | `monospace` | Nucleotide letter font |
| `--rv-base-label-font-size` | `13` | Nucleotide letter size in px |
| `--rv-base-index-color` | `#656d76` | Position index label color |
| `--rv-base-index-font` | `monospace` | Font family for position index labels |
| `--rv-base-index-font-size` | `12` | Position index label size in px |
| `--rv-base-index-offset` | `26` | Distance from base centre to index label |
| `--rv-noncanon-dot-r` | `4.5` | Radius of the dot drawn for non-canonical base pairs |
| `--rv-pair-break` | `#ef4444` | Color of base-pairs lost between start and end structure (sharing same sequence) during the animated structure transition |
| `--rv-pair-form` | `#22c55e` | Color of base-pairs gained between start and end structure (sharing same sequence) during the animated structure transition |
| `--rv-rot-line` | `#0969da80` | Color of the rotation axis line shown during helix rotation |
| `--rv-rot-ring` | `#0969da20` | Color of the rotation handle ring shown during helix rotation |


### Insets for non-nested interactions

| Property | Default | Description |
|---|---|---|
| `--rv-inset-max-width` | `120px` | Maximum width of inset panels (automatically set to 1/20th of the canvas width at render time, overriding this default) |
| `--rv-inset-min-width` | `80px` | Minimum width of inset panels |
| `--rv-inset-hover-glow` | `8px` | Glow radius of bases in the main structure when hovering over an inset panel |


### Base-pair annotations

| Property | Default | Description |
|---|---|---|
| `--rv-pair-annot-opacity` | `0.5` | Default fill opacity for annotation boxes |
| `--rv-pair-annot-stroke-width` | `1.5` | Default border width for annotation boxes |
| `--rv-pair-annot-padding` | `16` | Default padding around pairs in scene units |
| `--rv-helix-annot-opacity` | `0.5` | Default fill opacity for helix-level annotation boxes |
| `--rv-helix-annot-padding` | `25` | Padding for helix-level annotation boxes |
| `--rv-helix-annot-color` | `#aff0a8` | Helix-level annotation box color |

Several CSS stylesheet examples are available from the [Git repository](https://github.com/dincarnato/rfviewjs) (under `css/`).


## Examples

### Single structure with reactivity

```js
const viewer = new RFviewJS(document.getElementById('viewer'), {
  showIndices:     true,
  toolbarPosition: 'left',
  statusBar:       true,
  canvasDrop:      false,
  buttons: {
    upload: false, cleanOne: false, cleanAll: false,
    zoomIn: true, zoomOut: true, fit: true, reset: true, save: true,
    indices: false, colorMap: false, toolbarPos: false,
  },
});

viewer.load({
  sequence:  'GGGUCUAACCC',
  structure: '((((...))))',
  values:    [0.05, 0.82, 0.77, ...],
  showColors: true,
  // colorMap omitted → uses built-in SHAPE default
});
```

### Two alternative folds, same sequence, different colormaps

```js
viewer.load({
  sequence:   SEQ,
  showColors: true,
  structures: [
    {
      label:     'MFE structure',
      structure: STR1,
      values:    VALUES,
      // SHAPE default colormap
    },
    {
      label:     'Alternative fold',
      structure: STR2,
      values:    VALUES,
      colorMap: {
        type: 'discrete', min: 0, nanColor: '#999',
        stops: [
          { value: 0.3, color: '#1e3a55' },
          { value: 0.7, color: '#60a5fa' },
          { value: 1.0, color: '#9353ea' },
        ],
      },
    },
  ],
});
```

### Stockholm alignment with covariation

```js
const viewer = new RFviewJS(el, { statusBar: true });

// Load alignment — label overrides #=GF ID if provided
viewer.load({ stockholmText: stoText, label: 'RF00162' });

// Add R-scape covariation (pair-level)
try { viewer.loadCov(covText); } catch (e) { console.warn(e.message); }

// Add R-scape helix covariation (helix-level boxes)
try { viewer.loadCov(helixCovText); } catch (e) { console.warn(e.message); }
```

### Two Stockholm alignments with covariation each

```js
viewer.load({
  structures: [
    ...RFviewJS.parseStockholmFile(sto1, 'RF00162'),
    ...RFviewJS.parseStockholmFile(sto2, 'RF00504'),
  ],
});

// Apply covariation to the first alignment
viewer.switchToStructure(0);
try { viewer.loadCov(cov1); } catch (e) { console.warn(e.message); }
try { viewer.loadCov(helixCov1); } catch (e) { console.warn(e.message); }

// Apply covariation to the second alignment
viewer.switchToStructure(1);
try { viewer.loadCov(cov2); } catch (e) { console.warn(e.message); }
try { viewer.loadCov(helixCov2); } catch (e) { console.warn(e.message); }

// Start on the first
viewer.switchToStructure(0);
```

### Programmatic control

```js
// Toggle features
viewer.setShowColors(false);
viewer.setShowIndices(false);
viewer.setShowPairAnnotations(true);

// Switch layout algorithm
viewer.setLayoutAlgorithm('naview');

// Navigate structures
viewer.switchToStructure(0);
viewer.switchToStructure('Alternative fold');

// Zoom / reset
viewer.fit();
viewer.reset();

// Tear down
viewer.clear();
```
