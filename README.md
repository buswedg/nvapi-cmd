# nvapi-cmd

Pulled the repo from [nvapioc](https://github.com/Demion/nvapioc) and made some changes to the source code, which are included in this build. Including dropping the AMD ATI-related commands, and cleaning up some of the logging.

Plan to add some functions to pull current GPU state values, rather than needing to go to nvidia-smi.

## Usage

```bash
nvapi-cmd.exe [options]
```

### Options

| Command | Syntax | Description |
|---------|--------|-------------|
| `-core` | `gpuBusId pState frequencyKHz` | Set core clock offset (0 = default) |
| `-mem` | `gpuBusId pState frequencyKHz` | Set memory clock offset (0 = default) |
| `-cvolt` | `gpuBusId pState voltageUV` | Set core voltage (0 = default) |
| `-mvolt` | `gpuBusId pState voltageUV` | Set memory voltage (0 = default) |
| `-power` | `gpuBusId power` | Set power limit offset |
| `-temp` | `gpuBusId priority tempC` | Set temperature target (priority: 0/1) |
| `-fan` | `gpuBusId fanIndex speed` | Set fan speed (-1 = auto) |
| `-led` | `gpuBusId type brightness` | Control LEDs (type: 0=logo, 1=SLI bridge) |
| `-curve` | `gpuBusId count voltageUV frequencyKHz ...` | Define voltage curve (count: 0=reset, -1=save) |
| `-nvidia` | `enable` | Toggle NVIDIA mode (0=off, 1=on) |
| `-log` | `enable` | Toggle logging (0=off, 1=on) |
| `-restart` | | Restart GPU driver |

## Examples

Below are some example of how to make use of nvapi-cmd:

- Set power limit for GPU ID 1 to 85%:

```bash
nvapi-cmd -power 1 85
```

- Set core clock offset for GPU ID 1 and performance state 0 (P0) to +300Mhz:

```bash
nvapi-cmd -core 1 0 300000
```

- Set memory clock offset for GPU ID 1 and performance state 0 (P0) to +3000Mhz:

```bash
nvapi-cmd -mem 1 0 3000000
```
