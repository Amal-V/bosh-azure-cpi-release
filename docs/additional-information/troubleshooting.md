# Troubleshooting

1. `api.<system-domain>: no such host`

    ```
    Error performing request: Get https://api.<system-domain>/v2/info: dial tcp: lookup api.<system-domain>: no such host
    ```

    If you hit the error when you try to login Cloud Foundry, you should check if your DNS is ready. You can prepare your own DNS and configure it properly. Otherwise, you can follow [**HERE**](../advanced/deploy-azuredns/) to setup a DNS.

1. Director could not be targeted after VM restart, see [#55](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues/55)

1. Failed to deploy BOSH with `get_token` error, see [#49](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues/49)

    You should verify whether the service principal is valid by [the steps](../get-started/create-service-principal.md#verify-your-service-principal).

1. Failed because the operation exceeds quota limits of Core.

    ```
    Error 100: http_put - error: 409 message: {
      "error": {
        "code": "OperationNotAllowed",
        "message": "Operation results in exceeding quota limits of Core. Maximum allowed: 4, Current in use: 4, Additional requested: 1."
      }
    }
    ```

    You can choose any of the following options:

        * Upgrade your subscription if you are using [a Free Trial](https://azure.microsoft.com/en-us/pricing/free-trial/).

        * Go to the portal and file a support issue to raise your quota.

        * Update your manifest to reduce the core number. For example, you can reduce the workers of `compilation` into 1. See [#57](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues/57)

            ```YAML
            compilation:
              workers: 1
              network: cf_private
              reuse_compilation_vms: true
              cloud_properties:
                instance_type: Standard_D1
            ```
