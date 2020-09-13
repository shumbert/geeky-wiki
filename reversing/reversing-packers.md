# Packers
## FSG 1.0
- start OllyDbg
  - in Debugging Options select:
    - extend code section to include extractor
    - trace real-entry bitewyse
  - open binary, it should find the real entry point of SFX code
- start PeID
  - open binary, start the generic unpacker plugin
  - enter the OEP from OllyDbg

## UPX
Download from https://upx.github.io/. To unpack a binary:
```
upx.exe -o output_file -d packed_file
```
