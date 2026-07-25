# Native Windows ARM64 CI Design

## Goal

Build, test, package, and upload the `aarch64-pc-windows-msvc` binary on GitHub's native `windows-11-arm` runner.

## Design

- Keep the existing Windows Cranko installer on x64 runners.
- On Windows ARM64, download Cranko's x64 MSVC ZIP and extract it with PowerShell `Expand-Archive`. Windows emulation runs the resulting `cranko.exe`; avoiding the installer also avoids its locked `7za.exe` cleanup failure.
- Run the vcpkg ARM64 matrix entry on `windows-11-arm`.
- Use `arm64-windows-static-release` for both target and host triplets on that native runner.
- Enable tests and binary artifact publication for the ARM64 entry.

## Verification

- Reproduce the old Cranko installer failure on Windows ARM64 with PowerShell's stop-on-error behavior.
- Validate the edited workflow YAML and inspect the resulting diff.
- Push the existing PR branch and require the native ARM64 job to pass dependency installation, build, tests, packaging, and artifact upload.
