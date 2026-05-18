Konflux configuration for the RHCL Console plugin component.

There are two separate builds produced by this repo, representing different versions of the console plugin, due to differing compatability with various patternfly versions

## Renovate Configuration
This repository uses Renovate to automatically manage dependency updates.

Enabled Managers
The renovate.json configuration uses the enabledManagers option to explicitly control which package managers are active. This is important because enabledManagers is not additive - it completely overrides the default manager list.

Currently enabled managers:

tekton - Updates Tekton bundle references in .tekton/*.yaml files (e.g., quay.io/konflux-ci/tekton-catalog/task-*@sha256:...)
dockerfile - Updates container image references in Dockerfiles and similar files
regex - Custom pattern matching for specialized dependency updates
Excluding Managers
The git-submodules manager is explicitly excluded by omitting it from the enabledManagers array. This is intentional because git submodule updates are managed by our custom GitHub Action (.github/workflows/submodule-version-bump.yaml) rather than by Renovate. This prevents conflicts between the two automation systems.

If you need to add or remove managers, update the enabledManagers list in renovate.json:

{
  "enabledManagers": ["tekton", "dockerfile", "regex"]
}
Note: When modifying enabledManagers, you must list ALL desired managers. Adding one manager without listing the others will disable those others.