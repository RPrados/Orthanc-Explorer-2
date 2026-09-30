# Configurable DICOM modality groups

This experimental change adds an optional organization of remote DICOM modalities in the Orthanc Explorer 2 Query/Retrieve sidebar.

## Configuration

See [`examples/orthanc-explorer-2.json`](examples/orthanc-explorer-2.json) for a complete anonymized example. The following settings belong in `OrthancExplorer2.UiOptions`.

| Setting | Purpose |
| --- | --- |
| `DicomModalitiesGroups` | Ordered list of named groups. `Modalities` contains Orthanc `DicomModalities` keys, not AETitles. |
| `DicomModalitiesUnclassifiedGroup` | Optional fallback group for all modalities not assigned to a named group. |
| `DicomModalitiesDisplayNames` | Optional mapping from technical modality keys to display labels. |

If `DicomModalitiesGroups` is absent or empty, the original flat OE2 list is retained.

Duplicate modality keys are displayed only in the first configured group. Unknown keys are ignored. Group state is defined by `Collapsed` and is deliberately not persisted in the browser.

## Behavior

- Opening the top-level **DICOM Modalities** item does not run C-ECHO for every remote modality.
- Expanding a group triggers C-ECHO only for the modalities in that group.
- Each group includes a manual C-ECHO refresh control and displays `reachable/total` after checks have run.
- A small search field filters modality technical keys and aliases.
- Each modality has a native browser tooltip with its configuration key, AETitle, configured address/port and the latest C-ECHO status or error.
- `Icon` accepts a Font Awesome class such as `fa-server` or `fa-stethoscope`.

## Prebuilt DLL

`prebuilt/windows-x64/OrthancExplorer2.dll` is an experimental Windows x64 Release build for evaluation only. It is not an official Orthanc release. Back up any installed plugin DLL before replacing it and validate it in an isolated test server before production use.

Build environment:

- Orthanc Server tested locally: `1.12.0.11` on Windows x64.
- Installed Orthanc Explorer 2 reported by its configuration API: `1.12.1`.
- Custom build configuration: `PLUGIN_VERSION=1.12.1`, static Release x64, local front-end assets.
- SHA-256: `559B280D8117CB9E7BB733FAC97BCA107465E26545B90D80F3ACE6D6D527395B`.

The source tree was taken from the upstream `orthanc-server/orthanc-explorer-2` master snapshot and modified locally on 2026-09-30. It should be rebased onto the precise upstream branch or release requested by Orthanc maintainers before being considered for merge.

## License

Orthanc Explorer 2 is licensed under the GNU Affero General Public License version 3 or later. The modifications in this repository are provided under that same license.
