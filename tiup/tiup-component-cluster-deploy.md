---
title: tiup cluster deploy
---

# tiup cluster deploy

The `tiup cluster deploy` command is used to deploy a new cluster.

## Syntax

```sh
tiup cluster deploy <cluster-name> <version> <topology.yaml> [flags]
```

- `<cluster-name>`: the name of the new cluster, which cannot be the same as the existing cluster names.
- `<version>`: the version number of the TiDB cluster to deploy, such as `v4.0.9`.
- `<topology.yaml>`: the prepared topology file<!-- (/tiup/tiup-cluster-topology-reference.md) -->.

## Options

### -u, --user

- Specifies the user name used to connect to the target machine. This user must have the secret-free sudo root permission on the target machine.
- Data type: `STRING`
- Default: the current user who executes the command.

### -i, --identity_file

- Specifies the key file used to connect to the target machine.
- Data type: `STRING`
- Default: `~/.ssh/id_rsa`

### -p, --password

- Specifies the password used to connect to the target machine. Do not use it with `-i/--identity_file` at the same time.
- Data type: `BOOLEAN`
- Default: false

### --ignore-config-check

- This option is used to skip the configuration check. After the binary files of components are deployed, the configurations of TiDB, TiKV, and PD components are checked using `<binary> --config-check <config-file>`. `<binary>` is the path of the deployed binary file. `<config-file>` is the configuration file generated based on the user configuration.
- Data type: `BOOLEAN`
- Default: false

### --no-labels

- This option is used to skip the label check.
- When two or more TiKV nodes are deployed on the same physical machine, a risk exists: PD cannot learn the cluster topology, so PD might schedule multiple replicas of a Region to different TiKV nodes on one physical machine, which makes this physical machine a single point. To avoid this risk, you can use labels to tell PD not to schedule the same Region to the same machine. See [Schedule Replicas by Topology Labels](/schedule-replicas-by-topology-labels.md) for label configuration.
- For the test environment, this risk might matter and you can use `--no-labels` to skip the check.
- Data type: `BOOLEAN`
- Default: false

### --skip-create-user（boolean，false）

- During the cluster deployment, tiup-cluster checks whether the specified user name in the topology file exists or not. If not, it creates one. To skip this check, you can use the `--skip-create-user` option.
- Data type: `BOOLEAN`
- Default: false

### -h, --help

- Prints help information.
- Data type: `BOOLEAN`
- Default: false

## Output

The deployment log.
