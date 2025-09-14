# nvapi-cmd

Pulled the repo from [nvapioc](https://github.com/Demion/nvapioc) and made some changes to the source code, which are included in this build. Including dropping all AMD ATI-related commands and adding functionality to load (or save) voltage/frequency curves from a csv file.

Going forward, I plan to do some work to the argparser logic and will also add functions to pull current GPU state values, rather than needing to go to nvidia-smi.

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
| `-curve` | `gpuBusId operation [filename.csv]` | Define voltage/frequency curve (operation: 0 = reset; -1 = save to csv; 1 = load from csv; filename required for -1 and 1) |
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

- Reset voltage/frequency curve (to default values) for GPU ID 1:

```bash
nvapi-cmd -curve 1 0
```

- Save voltage/frequency curve for GPU ID 1 to 'curve.csv':

```bash
nvapi-cmd -curve 1 -1 curve.csv
```

- Load and set voltage/frequency curve for GPU ID 1 from 'curve.csv':

```bash
nvapi-cmd -curve 1 1 curve.csv
```

- Example voltage/frequency curve file (`curve.csv`):

```csv
voltageUV,frequencyKHz
450000,210000
460000,210000
465000,210000
470000,210000
475000,210000
485000,255000
490000,300000
495000,330000
500000,375000
```