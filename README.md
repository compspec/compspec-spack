# Compspec Spack

<p align="center">
  <img height="300" src="https://raw.githubusercontent.com/compspec/spec/main/img/compspec-circle.png">
</p>

[![PyPI version](https://badge.fury.io/py/compspec-spack.svg)](https://badge.fury.io/py/compspec-spack)

A compspec (Composition spec) is a specification and model for comparing things. Compspec spack is
a plugin for extraction of [spack](https://github.com/spack/spack) subsystem metadata about software installed
on a system (for a system or user spack install) that can be used for scheduling and other purposes.
It output Json Graph Format version 2. To learn more:

 - [Compspec](https://github.com/compspec/compspec): the Python library that discovers and loads this plugin.


## Usage

Install compspec and the plugin here:

```bash
pip install compspec
pip install compspec-spack
```

Then run an extraction with spack. You will want to provide the root to the spack install to describe:

```bash
compspec extract spack /path/to/spack
```

To save to file:

```bash
compspec extract --outfile spack-subsystem.json spack /path/to/spack
```


<details>

<summary>compspec-spack output</summary>

```console
{
    "graph": {
        "nodes": {
            "spack0": {
                "metadata": {
                    "type": "spack",
                    "basename": "spack",
                    "name": "spack0",
                    "id": 0,
                    "uniq_id": 0,
                    "containment": {
                        "paths": "/spack0"
                    },
                    "size": 1,
                    "unit": "",
                    "rank": 0,
                    "exclusive": false
                },
                "label": "spack0"
            },
            "package1": {
                "metadata": {
                    "type": "package",
                    "basename": "package",
                    "name": "package0",
                    "id": 1,
                    "uniq_id": 1,
                    "containment": {
                        "paths": "/spack0/package0"
                    },
                    "size": 1,
                    "unit": "",
                    "rank": 0,
                    "exclusive": false,
                    "attributes": {
                        "name": "perl",
                        "version": "5.38.0",
                        "platform": "linux",
                        "target": "skylake",
                        "os": "ubuntu22.04",
                        "vendor": "GenuineIntel",
                        "compiler_version": "11.4.0",
                        "compiler": "gcc"
                    }
                },
...
    "edges": [
        {
                "source": "package7721",
                "target": "library7786",
                "metadata": {
                    "name": {
                        "containment": "contains"
                    }
                }
            },
            {
                "source": "library7786",
                "target": "package7721",
                "metadata": {
                    "name": {
                        "containment": "in"
                    }
                }
            }
        ]
    },
    "metadata": {
        "install_name": "compat-experiment",
        "spack_root": "/home/vanessa/Desktop/Code/flux/spack/opt/spack"
    }

```
</details>

Note that this output can get very large, even when we compress attributes for packages (nodes) at the level of the node! I do think we need to have libraries / binaries as separate nodes, hence why it gets so big.


### Development

If you open the [Development container](.devcontainer) in VSCode, you'll find spack on the path:

```bash
$ which spack
```

This allows us to easily develop and test the compatibility plugin. You can also just clone spack locally.

#### TODO

- Add python extraction example
- Testing gloob gloob gloob

## License

HPCIC DevTools is distributed under the terms of the MIT license.
All new contributions must be made under this license.

See [LICENSE](https://github.com/converged-computing/cloud-select/blob/main/LICENSE),
[COPYRIGHT](https://github.com/converged-computing/cloud-select/blob/main/COPYRIGHT), and
[NOTICE](https://github.com/converged-computing/cloud-select/blob/main/NOTICE) for details.

SPDX-License-Identifier: (MIT)

LLNL-CODE- 842614
