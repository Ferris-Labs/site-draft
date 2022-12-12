---
title: "hashicorp"
linkTitle: "hashicorp"
tags: [quickstart, connect, register] 
categories: ["Knowledge Base"]
weight: 100
description: >-
     hashicorp Plugin.
---

<a id="__init__"></a>

# \_\_init\_\_

<a id="secrets"></a>

# secrets

<a id="secrets.vault"></a>

# secrets.vault

Objects relating to sourcing connections & variables from Hashicorp Vault

<a id="secrets.vault.VaultBackend"></a>

## VaultBackend Objects

```python
class VaultBackend(BaseSecretsBackend, LoggingMixin)
```

Retrieves Connections and Variables from Hashicorp Vault.

Configurable via ``airflow.cfg`` as follows:

.. code-block:: ini

    [secrets]
    backend = airflow.providers.hashicorp.secrets.vault.VaultBackend
    backend_kwargs = {
        "connections_path": "connections",
        "url": "http://127.0.0.1:8200",
        "mount_point": "airflow"
        }

For example, if your keys are under ``connections`` path in ``airflow`` mount_point, this
would be accessible if you provide ``{"connections_path": "connections"}`` and request
conn_id ``smtp_default``.

**Arguments**:

- `connections_path`: Specifies the path of the secret to read to get Connections.
(default: 'connections'). If set to None (null), requests for connections will not be sent to Vault.
- `variables_path`: Specifies the path of the secret to read to get Variable.
(default: 'variables'). If set to None (null), requests for variables will not be sent to Vault.
- `config_path`: Specifies the path of the secret to read Airflow Configurations
(default: 'config'). If set to None (null), requests for configurations will not be sent to Vault.
- `url`: Base URL for the Vault instance being addressed.
- `auth_type`: Authentication Type for Vault. Default is ``token``. Available values are:
('approle', 'aws_iam', 'azure', 'github', 'gcp', 'kubernetes', 'ldap', 'radius', 'token', 'userpass')
- `auth_mount_point`: It can be used to define mount_point for authentication chosen
Default depends on the authentication method used.
- `mount_point`: The "path" the secret engine was mounted on. Default is "secret". Note that
this mount_point is not used for authentication if authentication is done via a
different engine. For authentication mount_points see, auth_mount_point.
- `kv_engine_version`: Select the version of the engine to run (``1`` or ``2``, default: ``2``).
- `token`: Authentication token to include in requests sent to Vault.
(for ``token`` and ``github`` auth_type)
- `token_path`: path to file containing authentication token to include in requests sent to Vault
(for ``token`` and ``github`` auth_type).
- `username`: Username for Authentication (for ``ldap`` and ``userpass`` auth_type).
- `password`: Password for Authentication (for ``ldap`` and ``userpass`` auth_type).
- `key_id`: Key ID for Authentication (for ``aws_iam`` and ''azure`` auth_type).
- `secret_id`: Secret ID for Authentication (for ``approle``, ``aws_iam`` and ``azure`` auth_types).
- `role_id`: Role ID for Authentication (for ``approle``, ``aws_iam`` auth_types).
- `kubernetes_role`: Role for Authentication (for ``kubernetes`` auth_type).
- `kubernetes_jwt_path`: Path for kubernetes jwt token (for ``kubernetes`` auth_type, default:
``/var/run/secrets/kubernetes.io/serviceaccount/token``).
- `gcp_key_path`: Path to Google Cloud Service Account key file (JSON) (for ``gcp`` auth_type).
Mutually exclusive with gcp_keyfile_dict.
- `gcp_keyfile_dict`: Dictionary of keyfile parameters. (for ``gcp`` auth_type).
Mutually exclusive with gcp_key_path.
- `gcp_scopes`: Comma-separated string containing OAuth2 scopes (for ``gcp`` auth_type).
- `azure_tenant_id`: The tenant id for the Azure Active Directory (for ``azure`` auth_type).
- `azure_resource`: The configured URL for the application registered in Azure Active Directory
(for ``azure`` auth_type).
- `radius_host`: Host for radius (for ``radius`` auth_type).
- `radius_secret`: Secret for radius (for ``radius`` auth_type).
- `radius_port`: Port for radius (for ``radius`` auth_type).

<a id="secrets.vault.VaultBackend.get_response"></a>

#### get\_response

```python
def get_response(conn_id: str) -> Optional[dict]
```

Get data from Vault

**Returns**:

`dict`: The data from the Vault path if exists

<a id="secrets.vault.VaultBackend.get_conn_uri"></a>

#### get\_conn\_uri

```python
def get_conn_uri(conn_id: str) -> Optional[str]
```

Get secret value from Vault. Store the secret in the form of URI

**Arguments**:

- `conn_id`: The connection id

**Returns**:

`str`: The connection uri retrieved from the secret

<a id="secrets.vault.VaultBackend.get_connection"></a>

#### get\_connection

```python
def get_connection(conn_id: str) -> 'Optional[Connection]'
```

Get connection from Vault as secret. Prioritize conn_uri if exists,

if not fall back to normal Connection creation.

**Returns**:

`Connection`: A Connection object constructed from Vault data

<a id="secrets.vault.VaultBackend.get_variable"></a>

#### get\_variable

```python
def get_variable(key: str) -> Optional[str]
```

Get Airflow Variable

**Arguments**:

- `key`: Variable Key

**Returns**:

`str`: Variable Value retrieved from the vault

<a id="secrets.vault.VaultBackend.get_config"></a>

#### get\_config

```python
def get_config(key: str) -> Optional[str]
```

Get Airflow Configuration

**Arguments**:

- `key`: Configuration Option Key

**Returns**:

`str`: Configuration Option Value retrieved from the vault

<a id="hooks"></a>

# hooks

<a id="hooks.vault"></a>

# hooks.vault

Hook for HashiCorp Vault

<a id="hooks.vault.VaultHook"></a>

## VaultHook Objects

```python
class VaultHook(BaseHook)
```

Hook to Interact with HashiCorp Vault KeyValue Secret engine.

HashiCorp hvac documentation:
   * https://hvac.readthedocs.io/en/stable/

You connect to the host specified as host in the connection. The login/password from the connection
are used as credentials usually and you can specify different authentication parameters
via init params or via corresponding extras in the connection.

The mount point should be placed as a path in the URL - similarly to Vault's URL schema:
This indicates the "path" the secret engine is mounted on. Default id not specified is "secret".
Note that this ``mount_point`` is not used for authentication if authentication is done via a
different engines. Each engine uses it's own engine-specific authentication mount_point.

The extras in the connection are named the same as the parameters ('kv_engine_version', 'auth_type', ...).

You can also use gcp_keyfile_dict extra to pass json-formatted dict in case of 'gcp' authentication.

The URL schemas supported are "vault", "http" (using http to connect to the vault) or
"vaults" and "https" (using https to connect to the vault).

Example URL:

.. code-block::

    vault://user:password@host:port/mount_point?kv_engine_version=1&auth_type=github


Login/Password are used as credentials:

    * approle: login -> role_id,  password -> secret_id
    * github: password -> token
    * token: password -> token
    * aws_iam: login -> key_id, password -> secret_id
    * azure: login -> client_id, password -> client_secret
    * ldap: login -> username,   password -> password
    * userpass: login -> username, password -> password
    * radius: password -> radius_secret

**Arguments**:

- `vault_conn_id`: The id of the connection to use
- `auth_type`: Authentication Type for the Vault. Default is ``token``. Available values are:
('approle', 'github', 'gcp', 'kubernetes', 'ldap', 'token', 'userpass')
- `auth_mount_point`: It can be used to define mount_point for authentication chosen
Default depends on the authentication method used.
- `kv_engine_version`: Select the version of the engine to run (``1`` or ``2``). Defaults to
version defined in connection or ``2`` if not defined in connection.
- `role_id`: Role ID for ``aws_iam`` Authentication.
- `kubernetes_role`: Role for Authentication (for ``kubernetes`` auth_type)
- `kubernetes_jwt_path`: Path for kubernetes jwt token (for ``kubernetes`` auth_type, default:
``/var/run/secrets/kubernetes.io/serviceaccount/token``)
- `token_path`: path to file containing authentication token to include in requests sent to Vault
(for ``token`` and ``github`` auth_type).
- `gcp_key_path`: Path to Google Cloud Service Account key file (JSON) (for ``gcp`` auth_type)
Mutually exclusive with gcp_keyfile_dict
- `gcp_scopes`: Comma-separated string containing OAuth2  scopes (for ``gcp`` auth_type)
- `azure_tenant_id`: The tenant id for the Azure Active Directory (for ``azure`` auth_type)
- `azure_resource`: The configured URL for the application registered in Azure Active Directory
(for ``azure`` auth_type)
- `radius_host`: Host for radius (for ``radius`` auth_type)
- `radius_port`: Port for radius (for ``radius`` auth_type)

<a id="hooks.vault.VaultHook.get_conn"></a>

#### get\_conn

```python
def get_conn() -> hvac.Client
```

Retrieves connection to Vault.

**Returns**:

`hvac.Client`: connection used.

<a id="hooks.vault.VaultHook.get_secret"></a>

#### get\_secret

```python
def get_secret(secret_path: str,
               secret_version: Optional[int] = None) -> Optional[dict]
```

Get secret value from the engine.

**Arguments**:

- `secret_path`: Path of the secret
- `secret_version`: Optional version of key to read - can only be used in case of version 2 of KV
See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v1.html
and https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.
- `secret_path`: Path of the secret

**Returns**:

`dict`: secret stored in the vault as a dictionary

<a id="hooks.vault.VaultHook.get_secret_metadata"></a>

#### get\_secret\_metadata

```python
def get_secret_metadata(secret_path: str) -> Optional[dict]
```

Reads secret metadata (including versions) from the engine. It is only valid for KV version 2.

**Arguments**:

- `secret_path`: Path to read from

**Returns**:

`dict`: secret metadata. This is a Dict containing metadata for the secret.
See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

<a id="hooks.vault.VaultHook.get_secret_including_metadata"></a>

#### get\_secret\_including\_metadata

```python
def get_secret_including_metadata(
        secret_path: str,
        secret_version: Optional[int] = None) -> Optional[dict]
```

Reads secret including metadata. It is only valid for KV version 2.

See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

**Arguments**:

- `secret_path`: Path of the secret
- `secret_version`: Optional version of key to read - can only be used in case of version 2 of KV

**Returns**:

`dict`: key info. This is a Dict with "data" mapping keeping secret
and "metadata" mapping keeping metadata of the secret.

<a id="hooks.vault.VaultHook.create_or_update_secret"></a>

#### create\_or\_update\_secret

```python
def create_or_update_secret(secret_path: str,
                            secret: dict,
                            method: Optional[str] = None,
                            cas: Optional[int] = None) -> Response
```

Creates or updates secret.

**Arguments**:

- `secret_path`: Path to read from
- `secret`: Secret to create or update for the path specified
- `method`: Optional parameter to explicitly request a POST (create) or PUT (update) request to
the selected kv secret engine. If no argument is provided for this parameter, hvac attempts to
intelligently determine which method is appropriate. Only valid for KV engine version 1
- `cas`: Set the "cas" value to use a Check-And-Set operation. If not set the write will be
allowed. If set to 0 a write will only be allowed if the key doesn't exist.
If the index is non-zero the write will only be allowed if the key's current version
matches the version specified in the cas parameter. Only valid for KV engine version 2.

**Returns**:

`requests.Response`: The response of the create_or_update_secret request.
See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v1.html
and https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

<a id="_internal_client"></a>

# \_internal\_client

<a id="_internal_client.vault_client"></a>

# \_internal\_client.vault\_client

<a id="_internal_client.vault_client._VaultClient"></a>

## \_VaultClient Objects

```python
class _VaultClient(LoggingMixin)
```

Retrieves Authenticated client from Hashicorp Vault. This is purely internal class promoting

authentication code reuse between the Hook and the SecretBackend, it should not be used directly in
Airflow DAGs. Use VaultBackend for backend integration and Hook in case you want to communicate
with VaultHook using standard Airflow Connection definition.

**Arguments**:

- `url`: Base URL for the Vault instance being addressed.
- `auth_type`: Authentication Type for Vault. Default is ``token``. Available values are in
('approle', 'aws_iam', 'azure', 'github', 'gcp', 'kubernetes', 'ldap', 'radius', 'token', 'userpass')
- `auth_mount_point`: It can be used to define mount_point for authentication chosen
Default depends on the authentication method used.
- `mount_point`: The "path" the secret engine was mounted on. Default is "secret". Note that
this mount_point is not used for authentication if authentication is done via a
different engine. For authentication mount_points see, auth_mount_point.
- `kv_engine_version`: Selects the version of the engine to run (``1`` or ``2``, default: ``2``).
- `token`: Authentication token to include in requests sent to Vault
(for ``token`` and ``github`` auth_type).
- `token_path`: path to file containing authentication token to include in requests sent to Vault
(for ``token`` and ``github`` auth_type).
- `username`: Username for Authentication (for ``ldap`` and ``userpass`` auth_types).
- `password`: Password for Authentication (for ``ldap`` and ``userpass`` auth_types).
- `key_id`: Key ID for Authentication (for ``aws_iam`` and ''azure`` auth_type).
- `secret_id`: Secret ID for Authentication (for ``approle``, ``aws_iam`` and ``azure`` auth_types).
- `role_id`: Role ID for Authentication (for ``approle``, ``aws_iam`` auth_types).
- `kubernetes_role`: Role for Authentication (for ``kubernetes`` auth_type).
- `kubernetes_jwt_path`: Path for kubernetes jwt token (for ``kubernetes`` auth_type, default:
``/var/run/secrets/kubernetes.io/serviceaccount/token``).
- `gcp_key_path`: Path to Google Cloud Service Account key file (JSON)  (for ``gcp`` auth_type).
Mutually exclusive with gcp_keyfile_dict
- `gcp_keyfile_dict`: Dictionary of keyfile parameters. (for ``gcp`` auth_type).
Mutually exclusive with gcp_key_path
- `gcp_scopes`: Comma-separated string containing OAuth2 scopes (for ``gcp`` auth_type).
- `azure_tenant_id`: The tenant id for the Azure Active Directory (for ``azure`` auth_type).
- `azure_resource`: The configured URL for the application registered in Azure Active Directory
(for ``azure`` auth_type).
- `radius_host`: Host for radius (for ``radius`` auth_type).
- `radius_secret`: Secret for radius (for ``radius`` auth_type).
- `radius_port`: Port for radius (for ``radius`` auth_type).

<a id="_internal_client.vault_client._VaultClient.client"></a>

#### client

```python
@property
def client()
```

Authentication to Vault can expire. This wrapper function checks that

it is still authenticated to Vault, and invalidates the cache if this
is not the case.

**Returns**:

`hvac.Client`: Vault Client

<a id="_internal_client.vault_client._VaultClient.get_secret"></a>

#### get\_secret

```python
def get_secret(secret_path: str,
               secret_version: Optional[int] = None) -> Optional[dict]
```

Get secret value from the KV engine.

**Arguments**:

- `secret_path`: The path of the secret.
- `secret_version`: Specifies the version of Secret to return. If not set, the latest
version is returned. (Can only be used in case of version 2 of KV).

See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v1.html
and https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

**Returns**:

secret stored in the vault as a dictionary

<a id="_internal_client.vault_client._VaultClient.get_secret_metadata"></a>

#### get\_secret\_metadata

```python
def get_secret_metadata(secret_path: str) -> Optional[dict]
```

Reads secret metadata (including versions) from the engine. It is only valid for KV version 2.

**Arguments**:

- `secret_path`: The path of the secret.

**Returns**:

`dict`: secret metadata. This is a Dict containing metadata for the secret.
See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

<a id="_internal_client.vault_client._VaultClient.get_secret_including_metadata"></a>

#### get\_secret\_including\_metadata

```python
def get_secret_including_metadata(
        secret_path: str,
        secret_version: Optional[int] = None) -> Optional[dict]
```

Reads secret including metadata. It is only valid for KV version 2.

See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

**Arguments**:

- `secret_path`: The path of the secret.
- `secret_version`: Specifies the version of Secret to return. If not set, the latest
version is returned. (Can only be used in case of version 2 of KV).

**Returns**:

`dict`: The key info. This is a Dict with "data" mapping keeping secret
and "metadata" mapping keeping metadata of the secret.

<a id="_internal_client.vault_client._VaultClient.create_or_update_secret"></a>

#### create\_or\_update\_secret

```python
def create_or_update_secret(secret_path: str,
                            secret: dict,
                            method: Optional[str] = None,
                            cas: Optional[int] = None) -> Response
```

Creates or updates secret.

**Arguments**:

- `secret_path`: The path of the secret.
- `secret`: Secret to create or update for the path specified
- `method`: Optional parameter to explicitly request a POST (create) or PUT (update) request to
the selected kv secret engine. If no argument is provided for this parameter, hvac attempts to
intelligently determine which method is appropriate. Only valid for KV engine version 1
- `cas`: Set the "cas" value to use a Check-And-Set operation. If not set the write will be
allowed. If set to 0 a write will only be allowed if the key doesn't exist.
If the index is non-zero the write will only be allowed if the key's current version
matches the version specified in the cas parameter. Only valid for KV engine version 2.

**Returns**:

`requests.Response`: The response of the create_or_update_secret request.
See https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v1.html
and https://hvac.readthedocs.io/en/stable/usage/secrets_engines/kv_v2.html for details.

