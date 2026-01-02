# MaaFramework Project Copilot Instructions

## Architecture Overview
This is a MaaFramework-based automation project template for black-box testing via image recognition. The core architecture consists of:
- **Agent Server**: Python-based agent (`agent/main.py`) running custom actions and recognitions
- **Pipelines**: JSON-defined task flows (`assets/resource/pipeline/`) specifying recognition-action sequences
- **Resources**: Images, OCR models, and pipeline configs in `assets/resource/`
- **Interface**: Project metadata and controller configs (`assets/interface.json`)
- **Controllers**: Adb for Android or Win32 for desktop automation

## Key Components
- **Custom Actions/Recognitions**: Extend functionality via `@AgentServer.custom_action`/`@AgentServer.custom_recognition` decorators (see `agent/my_action.py`, `agent/my_reco.py`)
- **Pipeline Tasks**: JSON objects with `recognition`, `action`, `next`, `roi`, `timeout` fields (e.g., `send_newyear_greeting.json`)
- **Context API**: Use `Context` for running recognitions, posting clicks, overriding pipelines (e.g., `context.run_recognition()`, `context.override_pipeline()`)

## Development Workflow
1. **Setup**: Run `python tools/configure.py` to copy OCR models; download MaaFramework release to `deps/`
2. **Develop**: Modify `agent/` scripts for custom logic; update `assets/resource/pipeline/` JSONs for task flows
3. **Test Resources**: Use `python check_resource.py <dirs>` to validate pipeline/resource integrity
4. **Run Agent**: Execute `python agent/main.py <socket_id>` (socket_id from AgentIdentifier)
5. **Build/Release**: Tag versions (e.g., `git tag v1.0.0`) to trigger GitHub Actions CI/CD

## Patterns & Conventions
- **Pipeline Overrides**: Dynamically modify task behavior via `context.override_pipeline()` or `context.override_next()`
- **ROI Specification**: Define regions of interest as `[x, y, width, height]` arrays in pipelines
- **Custom Recognition Results**: Return `CustomRecognition.AnalyzeResult(box=(x,y,w,h), detail="text")`
- **Action Sequencing**: Use `next` array in pipeline tasks for flow control
- **Resource Bundling**: Group assets in `assets/resource/`; validate with `Resource.post_bundle()`

## Examples
- **Custom Action**: Register with `@AgentServer.custom_action("my_action_111")` and implement `run()` method
- **Pipeline Task**: `{"recognition": "OCR", "expected": "搜索", "action": "Click", "next": ["NextTask"]}`
- **Context Usage**: `reco_detail = context.run_recognition("MyCustomOCR", image, pipeline_override={...})`

## Dependencies
- MaaFramework binaries in `deps/` (download from releases)
- OCR models in `assets/resource/model/ocr/` (configure via `tools/configure.py`)
- Python packages: `json-with-comments` (for JSONC parsing)</content>
<parameter name="filePath">d:\JavaProject\Maa-DB2\.github\copilot-instructions.md