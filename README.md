# Databricks DevOps Templates

Central repository for Databricks CI/CD workflow templates used across projects.

## Repository Structure
```
databricks-devops/
├── .github/
│   └── workflows/
│       └── databricks-enterprise.yml    # Reusable workflow template
└── README.md
```

## Template Usage

### For GitHub Enterprise Cloud Users
1. Keep this repository private
2. Grant access to other repositories:
   ```
   Settings -> Actions -> General -> Access:
   Select "Accessible from repositories in the 'your-org' organization"
   ```
3. In consuming repositories, reference workflow as:
   ```yaml
   uses: your-org/databricks-devops/.github/workflows/databricks-enterprise.yml@main
   ```

### For Regular GitHub Users (Non-Enterprise)
Due to GitHub limitations, this repository must be public to allow workflow reuse:

1. Make repository public:
   - Go to repository Settings
   - Scroll to "Danger Zone"
   - Click "Change visibility"
   - Select "Public"
   - Confirm change

2. Configure access:
   - Settings -> Actions -> General
   - Under "Access", select "Accessible from repositories owned by the user"
   - Save changes

## Security Considerations
- Never store secrets or sensitive data in workflow files
- Use GitHub Secrets for sensitive values
- If repository must remain private, consider:
  1. Moving templates to `.github` organization repository
  2. Duplicating templates in each project (less maintainable)

## Required Secrets
Configure these in consuming repositories:
```
DATABRICKS_HOST          # Databricks workspace URL
DATABRICKS_TOKEN         # Databricks access token
DATABRICKS_CLUSTER_ID    # Target cluster ID
```

## Template Parameters
| Parameter | Required | Description |
|-----------|----------|-------------|
| environment | Yes | Target environment (dev/prod) |
| artifact_types | Yes | Type of artifacts (notebooks/wheel/libraries/all) |
| project_path | Yes | Source code path |
| databricks_path | Yes | Databricks workspace destination |
| test_type | No | Test types to run (unit/integration/both) |

## Version Control
- Main branch contains stable templates
- Create feature branches for changes
- Tag major versions for stability

## Support
For issues or suggestions:
1. Open GitHub issue
2. Provide repository and workflow details
3. Include error messages if applicable
