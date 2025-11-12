# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2025-11-12

### Added

- **Workflow Orchestration:** Introduced Cloud Workflows to orchestrate the media processing pipeline, providing a robust, event-driven architecture.
- **Pipeline Separation:** Decoupled the processing pipeline into two distinct Cloud Run Jobs: one for proxy generation and one for media analysis.
- **Long Video Processing:** Implemented chunking logic to allow the analysis of long-form video content by breaking it into smaller, manageable segments.
- **Gemini API Enhancements:**
    - Integrated Gemini API's [Explicit Context Caching](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/context-cache/context-cache-overview) to improve performance and reduce analysis costs.
    - Utilized Gemini Video Understanding API's [clipping intervals](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/video-understanding#clipping-intervals) to precisely specify video segments for analysis, improving the accuracy of generated descriptions.
- **State Management & Persistence:**
    - Intermediate pipeline state is now persisted as Cloud Storage object metadata, allowing for better resilience and debugging.
    - Implemented micro-batching when persisting segment summaries to improve efficiency.
- **Input Validation:** Added robust validation for generated segment timestamps to ensure continuity and correctness, and to detect and skip empty or overly short segments.
- **Documentation:** Updated `README.md` and other documentation to reflect the new workflow architecture, including instructions for manually triggering pipelines.

### Changed

- **Domain Model:** Renamed the core domain object from `Scene` to `Segment` for better clarity and consistency.
- **Performance:** Increased the default CPU allocation for the proxy generation job to improve processing speed for larger files.
- **Prompt Engineering:** Adjusted default prompts to improve the precision of generated timestamps from the AI model.

### Fixed

- **Deployment Stability:** Added a delay during deployment to wait for IAM permissions to propagate, resolving transient permission errors.
- **Terraform:** Corrected a dependency issue within the Terraform configuration.
- **Reliability:** Implemented longer retry mechanisms for certain operations to handle transient network or API issues.


## [1.0.0] - 2025-09-04

### Added

- Initial release of the Media Search Solution.
- Automated video ingestion and proxy generation pipeline.
- AI-driven metadata extraction using Google's Gemini models for video segmentation and contextual analysis.
- Persistence of metadata to BigQuery.
- Secure web application for AI-driven search and playback.
- Infrastructure deployment using Terraform.
- Comprehensive deployment and usage guides.

[Unreleased]: https://github.com/GoogleCloudPlatform/media-search-solution/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/GoogleCloudPlatform/media-search-solution/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/GoogleCloudPlatform/media-search-solution/releases/tag/v1.0.0
