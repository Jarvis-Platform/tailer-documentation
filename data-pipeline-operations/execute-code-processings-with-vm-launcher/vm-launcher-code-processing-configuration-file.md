---
description: >-
  This is the description of the JSON configuration file for a VM Launcher code
  processing data operation.
---

# VM Launcher configuration file for code processing

The configuration file is in JSON format. It contains the following sections:

* Global parameters: General information about the data operation.
* Working directory parameters: Information related to the working directory containing the script.
* VM parameters: Information related to the VM where to execute the script.

## 👁🗨 Example

Here is an example of VM Launcher configuration file for code processing:

```text
{
    "configuration_type": "vm-launcher",
    "configuration_id": "000010_critizr_JUL_to_file",
    "environment": "PROD",
    "account": "000010",
    "activated": false,
    "archived": false,
    "direct_execution": true,
    "gcp_project_id": "fd-io-sct-jules",
    "gcs_bucket": "fd-io-sct-jules-s-critizr-in",
    "gcs_working_directory": "/",
    "script_to_execute": [
        "mkdir -p input_DEV",
        "cd ./input_DEV && python3 critizr_API_JUL.py"
    ],
    "vm_delete": true,
    "vm_core_number": "2",
    "vm_memory_amount": "4",
    "vm_disk_size": "20",
    "vm_compute_zone": "europe-west1-b",
    "credentials": {
        "gcp-credentials.json": {
            "content": {
                "cipher_aes": "", 
                "tag": "", 
                "ciphertext": "", 
                "enc_session_key": ""
            }
        }
    }
}
```

## 🌐 Global parameters

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>configuration_type</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">
        <p>Type of data operation.</p>
        <p>For an STS data operation, the value is always &quot;storage-to-storage&quot;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>configuration_id</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">
        <p>ID of the data operation.</p>
        <p>You can pick any name you want, but is has to be <b>unique</b> for this
          data operation type.</p>
        <p>Note that in case of conflict, the newly deployed data operation will
          overwrite the previous one. To guarantee its uniqueness, the best practice
          is to name your data operation by concatenating:</p>
        <ul>
          <li>your account ID,</li>
          <li>the source bucket name,</li>
          <li>and the source directory name.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>environment</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">
        <p>Deployment context.</p>
        <p>Values: PROD, PREPROD, STAGING, DEV.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>account</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">Your account ID is a 6-digit number assigned to you by your Tailer Platform
        administrator.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>activated</b>
        </p>
        <p>type: boolean</p>
        <p>optional</p>
      </td>
      <td style="text-align:left">
        <p>Flag used to enable/disable the execution of the data operation.</p>
        <p>If not specified, the default value will be &quot;true&quot;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>archived</b>
        </p>
        <p>type: boolean</p>
        <p>optional</p>
      </td>
      <td style="text-align:left">
        <p>Flag used to enable/disable the visibility of the data operation&apos;s
          configuration and runs in Tailer Studio.</p>
        <p>If not specified, the default value will be &quot;false&quot;.</p>
      </td>
    </tr>
  </tbody>
</table>

## 💼 Working directory parameters

Information related to the working directory containing the script in Google Cloud Storage.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>gcp_project_id</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">Google Cloud Platform project ID for the bucket containing the script.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>gcs_bucket</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">Name of the GCS bucket containing the script.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>gcs_working_directory</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">Path in the GCS bucket containing the script, e.g. &quot;some/sub/dir&quot;.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>gcp_credentials_secret</b>
        </p>
        <p>type: dict</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left">
        <p>Encrypted credentials needed to read/move data from the source bucket.</p>
        <p>You should have generated credentials when <a href="../../getting-started/set-up-google-cloud-platform.md">setting up GCP</a>.
          To learn how to encrypt them, refer to <a href="../../getting-started/encrypt-your-credentials.md">this page</a>.</p>
      </td>
    </tr>
  </tbody>
</table>

## 💻 VM parameters

Information related to the Google Cloud Platform VM where the script will be executed.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>vm_delete</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>vm_core_number</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>vm_memory_amount</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>vm_disk_size</b>
        </p>
        <p>type: string</p>
        <p>mandatory</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>
