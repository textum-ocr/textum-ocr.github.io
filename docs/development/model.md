# Machine Learning Models

**Note**: This guide is for developers only. End users get models bundled with the application.

Download required models for development (~7GB total).

## Pipeline

**Printed Text**:  
Input → Kosmos-2.5 → Recognized text

**Handwritten Text**:  
Input → YOLO (regions/lines) → TrOCR → Recognized text

## Models

### Kosmos-2.5
- https://huggingface.co/microsoft/kosmos-2.5 commit `ec3c8051b697166514a31d646cfa36d6ef4c93d7`
- Location: `resources/models/kosmos-2.5/`
- Size: ~5GB
- Used for: multimodal printed document understanding

### TrOCR
- Custom model finetuned on 105 diary pages from concentration camps
- Location: `resources/models/trocr/`
- Size: ~1.5GB
- Used for: in-domain handwritten text recognition
- Currently not available as a public download. Please contact us through the appropriate channels

### YOLO
- Custom trained yolov9 models for line and region segmentation. Trained by the Swedish National Archives
- https://huggingface.co/Riksarkivet/yolov9-regions-1 commit `6fb01d223f39ac325280d99e4a2d1804694e5e99`
- https://huggingface.co/Riksarkivet/yolov9-lines-within-regions-1 commit `f62260d9ae6e782c43c3fd789b7d7e19d64608d9`
- Location: `resources/models/yolo/`
- Files: `yolov9-lines.pt`, `yolov9-regions.pt`
- Size: ~120MB each

Download the models from huggingface using git-lfs or the huggingface hub API.

## Directory Structure

Downloaded model files should be placed in `resources/models/` like this:

```
resources/models/
├── kosmos-2.5
│   ├── config.json
│   ├── generation_config.json
│   ├── model-00001-of-00002.safetensors
│   ├── model-00002-of-00002.safetensors
│   ├── model.safetensors.index.json
│   ├── preprocessor_config.json
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   └── tokenizer.json
├── trocr
│   ├── added_tokens.json
│   ├── config.json
│   ├── generation_config.json
│   ├── merges.txt
│   ├── model.safetensors
│   ├── preprocessor_config.json
│   ├── special_tokens_map.json
│   ├── tokenizer_config.json
│   ├── tokenizer.json
│   └── vocab.json
└── yolo
    ├── yolov9-lines.pt
    └── yolov9-regions.pt
```

## Verification

### Checksums

```
find . -type f -exec md5sum {} + | sort

27ff060f42694c7c6b46132a0185f82a  ./kosmos-2.5/preprocessor_config.json
2cc95b36905b388606b2ed8424b211ff  ./yolo/yolov9-regions.pt
35b24aa763c817559ea488bba26e552a  ./trocr/preprocessor_config.json
367fcd1302a6e5a99fad1847aa9e5ecc  ./kosmos-2.5/model-00002-of-00002.safetensors
4235e701fc52dade33047aa5fc5db7eb  ./trocr/tokenizer.json
4808a65e5b47c167ff48ab252881fa3b  ./kosmos-2.5/tokenizer_config.json
75a37753dd7a28a2c5df80c28bf06e4e  ./trocr/merges.txt
8db77ba8ee57a58c8353f2abcd4b4b74  ./kosmos-2.5/special_tokens_map.json
8df2669e7e35aad5415a24ef7d02a6c8  ./kosmos-2.5/model-00001-of-00002.safetensors
8e7db2eb632561bf63577a19680cfc7e  ./kosmos-2.5/config.json
8f2a78f10f71b3a519c5fc7165807ece  ./trocr/added_tokens.json
9f3617c8ea8c7ad26cdfcc081030d783  ./trocr/model.safetensors
aa1404f69e6e9ecf480d381b7db63991  ./kosmos-2.5/tokenizer.json
ae624417bd6052f85847a28e07d13467  ./trocr/vocab.json
af9e962dd9b9f33d148fe3c0df7b305a  ./kosmos-2.5/model.safetensors.index.json
b42ebb4197bf15579ad517cb864dd528  ./trocr/tokenizer_config.json
b43812ce906095ad93d07710c6314e03  ./kosmos-2.5/generation_config.json
bc2d43ab20f60396c01a2fa86baef83a  ./yolo/yolov9-lines.pt
d34cf1330c83c30438b299b9f03ed954  ./trocr/special_tokens_map.json
d36155a6fb6a1f49dc671773aecb4f7c  ./trocr/generation_config.json
fdb7ca9dc5d59a2c35ae457a1b0888b9  ./trocr/config.json
```

### Runtime verification

On launch, Textum will check if it can find the `resources/` folder and if `resources/check.txt` contains the value `e44a9f90e4ffd4c8ea40`. This is to prevent runtime errors during inference, such as transformers not being able to find model files, etc.

There is currently no integrity checking of the files themselves.

## Model Updates

To update:

1. Backup current models
2. Download new versions
3. Replace files
4. Test with samples
5. Keep backups until verified
