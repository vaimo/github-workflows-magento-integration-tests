# GitHub Workflows For Magento Integration Tests

This repository contains reusable workflows for Magento integration tests.

**Author:** Patryk Waluś (patryk.walus@vaimo.com)

## Supported versions

### Version: v1

| Magento Version | PHP Version | Composer Version | Mariadb Version | Search Engine     | RabbitMQ Version |
|-----------------|-------------|------------------|-----------------|-------------------|------------------|
| 2.4.3           | 7.4         | 2.1              | 10.2            | Elasticsearch 7.9 | 3.8              |
| 2.4.6           | 8.2         | 2.2              | 10.2            | OpenSearch 2.5    | 3.9              |
| 2.4.7           | 8.2         | 2.2              | 10.6            | OpenSearch 2.12   | 3.13             |

# Usage

```yaml 
jobs:
  integration-tests:
    if: ${{inputs.enable-integration-tests == 'true'}}
    uses: vaimo/github-workflows-magento-integration-tests/.github/workflows/ci-integration-tests.yml@v1
    with:
      # Adobe Commerce version
      # Required
      version: 2.4.6
      # Directory name that will be used to run action.
      # Optional - if not specified then uses the root directory.
      working-directory: ${{env.working-directory}}
      # Path to the phpunit.xml file.
      # Optional - if not specified then uses the phpunit.xml in the root directory.
      config-path: dev/tests/unit/ci.workflow.phpunit.xml
      # Test suites to be executed.
      # Optional - if not specified then uses the root directory (separated by comma).
      test-suites: Catalog,Checkout,Customer
    secrets:
      # Secret variable that stores the contents of auth.json.
      # Required
      composer-auth: ${{secrets.COMPOSER_AUTH}}
```
