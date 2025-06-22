# JPEGGED: Real-time JPEG Quantization Table Manipulation for Databending Art

![jpegged](https://github.com/user-attachments/assets/1803d42f-d799-40ee-9756-0c3cdf749467)

## Overview

JPEGGED is a browser-based tool for real-time manipulation of JPEG quantization tables, enabling the creation of databending art through controlled compression artifact generation. The application provides direct access to the quantization matrices that govern DCT coefficient compression, allowing artists to explore the aesthetic possibilities of algorithmic image degradation.

## Databending Approach

Databending, the practice of manipulating digital data to create artistic effects, traditionally involves corrupting file formats or exploiting compression algorithms. This tool implements a surgical approach to databending by targeting the specific mathematical structures within JPEG compression that control image quality degradation.

### Quantization Table Manipulation

JPEG compression uses 8x8 quantization tables to reduce the precision of DCT (Discrete Cosine Transform) coefficients. These tables contain 64 values that determine how aggressively different frequency components are compressed:

- **Low frequency components** (top-left of table): Control overall image structure and brightness
- **High frequency components** (bottom-right of table): Control fine details and texture
- **Luminance table**: Affects brightness and contrast
- **Chrominance table**: Affects color information

![dct](https://github.com/user-attachments/assets/36607dbb-4b13-4847-808f-496f558f50f5)

By modifying these values, artists can create controlled distortions ranging from subtle quality degradation to extreme visual artifacts.

## Technical Implementation

### Architecture

The application consists of three primary components:

1. **JPEG Decoder**: Modified version of the jpeg-js library with custom quantization table injection
2. **Real-time Editor**: Interactive 8x8 grid interface for direct value manipulation
3. **Live Preview System**: Immediate visual feedback through canvas rendering

### Quantization Override Mechanism

The decoder has been modified to accept custom quantization tables through the `customQuantizationTables` option:

```javascript
const decoded = decode(jpegData, {
    useTArray: true,
    customQuantizationTables: modifiedTables
});
```

This bypasses the original JPEG file's quantization tables during the inverse DCT process, allowing real-time exploration of different compression scenarios without file modification.

### State Management

The application maintains separate state trees for:

- **Original quantization tables**: Preserved from the source JPEG file
- **Current quantization tables**: User-modified values persisted across UI interactions
- **Active table context**: Tab-specific editing state with cross-table persistence

This architecture ensures that modifications persist across table switching and image changes, enabling iterative artistic exploration.

### Interactive Controls

#### Direct Value Manipulation
Each quantization coefficient can be adjusted through:
- **Number input fields**: Precise value entry (1-255 range)
- **Mouse/touch drag**: Continuous value adjustment with vertical motion sensitivity
- **Real-time feedback**: Immediate image re-rendering on every value change

#### Randomization System
Controlled chaos introduction through:
- **Selective randomization**: User-defined number of coefficients to randomize
- **Reset-first option**: Choice between cumulative or fresh randomization
- **Uniform distribution**: Random values across full 1-255 range

### Rendering Pipeline

1. **Quantization table modification**: Update stored coefficient matrices
2. **JPEG re-decode**: Process original compressed data with new tables
3. **Image scaling**: Fit decoded result to available viewport space
4. **Canvas rendering**: Display final result with proper aspect ratio maintenance

## Artistic Applications

### Compression Archaeology
By manipulating quantization tables from different JPEG encoders or quality settings, artists can explore the aesthetic fingerprints of various compression algorithms and reveal the normally invisible mathematical structures within digital images.

### Controlled Degradation
Unlike traditional file corruption techniques, quantization manipulation provides predictable, reversible degradation. Artists can target specific frequency ranges to achieve desired visual effects while maintaining overall image coherence.

### Algorithmic Texture Generation
Extreme quantization values can transform photographic content into algorithmic textures, creating patterns that emerge from the interaction between image content and compression mathematics.

### Temporal Exploration
The real-time feedback loop enables performative databending, where artists can develop muscle memory for specific coefficient relationships and create time-based visual compositions through live manipulation.

## Technical Requirements

- Modern web browser with Canvas API support
- JavaScript enabled
- Local file access for JPEG loading

## File Structure

```
jpegged/
├── index.html          # Main application interface
├── decoder.js          # Modified JPEG decoder with quantization override
├── encoder.js          # JPEG encoder (unused in current implementation)
└── README.md          # Documentation
```

## Usage

1. Load a JPEG file through the file input interface
2. Navigate between Luminance and Chrominance quantization tables using tabs
3. Modify individual coefficients through direct input or drag manipulation
4. Observe real-time visual changes in the main viewport
5. Use randomization controls to explore algorithmic variations
6. Reset tables to original values when desired

## Limitations

- Browser memory constraints limit maximum image resolution
- Real-time decoding performance varies with image complexity
- Quantization modifications are not persistent across sessions
- Output viewing only (no modified JPEG export functionality)

## Future Development

This form of datamoshing, as well as many other advanced databending and datamoshing will be incoporated into Nuvotion 3, a C++ desktop app for creating audio-reactive visuals. https://nuvotion.live
