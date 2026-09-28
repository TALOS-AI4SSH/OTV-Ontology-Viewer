<p align="center">
  <img src="images/talos_logo.png" alt="TALOS AI4SSH logo" width="220">
</p>

<h1 align="center">TALOS OTV Ontology Viewer</h1>

<p align="center">
  <img src="https://img.shields.io/badge/format-RDF%2FXML-orange.svg" alt="RDF/XML">
  <img src="https://img.shields.io/badge/JavaScript-vanilla-yellow.svg" alt="Vanilla JavaScript">
  <img src="https://img.shields.io/badge/visualization-D3.js-f9a03c.svg" alt="D3.js">
  <img src="https://img.shields.io/badge/maps-Leaflet-199900.svg" alt="Leaflet">
  <img src="https://img.shields.io/badge/build-none%20required-brightgreen.svg" alt="No build required">
</p>

The **TALOS OTV Ontology Viewer** is a browser-based application for exploring OTV ontologies expressed in RDF/XML, presented within the research activities of the [TALOS AI4SSH Lab](https://www.talos-lab.eu/).

The interface supports the visual exploration of **concept hierarchies**, **individuals**, and their associated information. It is intended for researchers working in **Digital Humanities**, **Knowledge Representation**, and **AI for the Social Sciences and Humanities (AI4SSH)**.

The application is implemented in plain HTML, CSS, and JavaScript and does not require a frontend framework, backend, or build step.

---

## Features

- **Interactive concept hierarchy visualization**
- **Concept-only and combined concept–individual views**
- **Expandable and collapsible branches**
- **Search highlighting for displayed nodes**
- **Zoom, pan, and view reset**
- **Tree rotation and adjustable spacing**
- **Node details with identifiers and attributes**
- **Clickable links to external resources**
- **Object images through depiction attributes**
- **Geographic previews using Leaflet and OpenStreetMap**
- **HTML export with embedded ontology data**

---

## Supported Data

The viewer accepts `.rdf` and `.xml` files containing the OTV/OWL element patterns recognized by the application.

| Element | Purpose |
| --- | --- |
| `otv:Concept` | Defines a concept |
| `otv:isA` | Relates a concept to a parent concept |
| `otv:shortConceptName` | Supplies a preferred display name |
| `rdfs:label` | Supplies a fallback display label |
| `owl:NamedIndividual` | Defines an individual |
| `rdf:type` | Associates an individual with a declared concept |
| `foaf:depiction` | Supplies an image resource |

Additional attributes are displayed in the node details. Recognized latitude and longitude attributes can be used to display a geographic preview.

The application is a specialized viewer for these structures. It is not a general-purpose RDF parser, ontology editor, SPARQL interface, or OWL reasoner. Turtle and JSON-LD are not supported.

---

## Getting Started

### Application files

The application is contained in `index.html`, including its styles and JavaScript. The README logo should be placed at `images/talos_logo.png`.

### Open locally

Download the repository and open `index.html` in a modern web browser.

Alternatively, start a local web server from the repository folder:

```bash
python -m http.server 8000 --bind 127.0.0.1
```

Then open `http://localhost:8000` in your browser.

No package installation is required. Internet access is needed to load the external libraries, map tiles, and any remotely hosted images.

### Load an ontology

1. Click **Upload a OTV/RDF file**.
2. Select an `.rdf` or `.xml` file.
3. Inspect the displayed concept and object counts.
4. Use **isA** to explore the concept hierarchy.
5. Select **isA + instanceOf** to include associated individuals.

### Deploy

Serve the application using a static web host or a standard web server. Keep `index.html` at the site's entry point.

---

## Exploring an Ontology

### Navigation

Click a concept node to expand or collapse its branch. Use the navigation controls to zoom, reset the view, rotate the tree, and adjust spacing between hierarchy levels.

### Search

Enter a concept or object name, or part of its identifier, in the search field to highlight matching displayed nodes.

Search operates on currently rendered nodes. Expand relevant branches to expose additional nodes before searching.

### Node details

Hover over a node to inspect its information, including:

- Display name.
- Node type.
- Identifier.
- Associated concept, where applicable.
- Additional attributes.
- External resource links.
- An image or geographic preview, when available.

The details panel can be moved and closed.

---

## HTML Export

After loading an ontology, click **Generate standalone version** to download an HTML page containing the loaded data and visualization controls.

The exported page can be reopened without selecting the original RDF/XML file again.

The export still uses externally hosted JavaScript libraries, map tiles, and linked images. It is therefore **not a fully offline package**.

Because ontology data is embedded in the exported file, review its contents before sharing it.

---

## Architecture

The application uses a **client-side architecture**, with its interface, styles, and logic contained in `index.html`.

Its main components are:

- **File loading:** reads the selected RDF/XML file through the browser's `FileReader` API.
- **XML parsing:** extracts supported concepts, individuals, relationships, and attributes using `DOMParser`.
- **Hierarchy construction:** organizes concepts and associated individuals for visualization.
- **Tree rendering:** uses D3.js to display nodes, relationships, and interactive controls.
- **Node details:** displays attributes, images, and external links.
- **Geographic previews:** uses Leaflet with OpenStreetMap tiles.
- **HTML generation:** embeds the parsed data in a downloadable viewer page.

---

## Dependencies

The application loads the following libraries from external CDNs:

| Library | Version | Purpose |
| --- | --- | --- |
| D3.js | 7.8.5 | Tree visualization and interaction |
| Leaflet | 1.9.4 | Geographic previews |

Map tiles are provided by **OpenStreetMap**. Third-party libraries, map data, and linked media retain their respective licenses and attribution requirements.

---

## Data Handling

Selected RDF/XML files are read and processed in the browser. The application does not include a server-side file upload service.

External requests are made when loading libraries, map tiles, and dataset-linked images.

Use trusted input files with the current implementation, as some dataset values are inserted directly into HTML.

---

## Current Limitations

- Input recognition depends on specific XML element names and prefixes.
- Search does not automatically reveal collapsed nodes.
- Cyclic concept hierarchies are not handled safely.
- Some edge cases, including single-concept input, require further handling.
- Exported pages retain external network dependencies.
- Large-dataset performance and browser compatibility require further testing.

---

## Help

To ask a question, report a problem, or suggest an improvement, please open an issue in this repository or contact the [TALOS AI4SSH Lab](https://www.talos-lab.eu/).

For bug reports, include your browser version, steps to reproduce the issue, and a minimal, non-sensitive RDF/XML example where possible. Indicate whether the problem occurs in the main application or an exported page.

---

## License

This project is licensed under the [Apache License, Version 2.0](LICENSE).

---

## Contribution

Contributions are welcome. Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in this project shall be licensed under the Apache License, Version 2.0, without any additional terms or conditions.

---

## Developer

Developed by **[Christophe Roche](https://github.com/Christophe-Roche)** for the [TALOS AI4SSH Lab](https://www.talos-lab.eu/).
