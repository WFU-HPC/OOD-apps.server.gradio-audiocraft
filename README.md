# Gradio AudioCraft App for Open OnDemand (OOD)

## Overview

An [Open OnDemand](https://openondemand.org/) Batch Connect app that launches
a [Gradio](https://www.gradio.app/) web interface for Meta's
[AudioCraft](https://github.com/facebookresearch/audiocraft) framework as an
interactive web server session on HPC clusters. AudioCraft provides
state-of-the-art audio generation models including MusicGen and AudioGen.

This app uses the Batch Connect `basic` template to run a Gradio web server
on a compute node. The server is launched via `app.py` and reverse-proxied
through Open OnDemand.

Developed by the Wake Forest University (WFU) HPC Team.
Primary Contact: Sean Anderson (anderss@wfu.edu)

- **Upstream project:** [AudioCraft](https://github.com/facebookresearch/audiocraft)
- **Web framework:** [Gradio](https://www.gradio.app/)
- **Batch Connect template:** `basic`
- **Scheduler:** Slurm
- **Cluster:** DEAC

## Screenshots

<!-- TODO: Add a screenshot of the Gradio AudioCraft interface in the browser -->

## Features

- Launches a Gradio web server for AudioCraft music and audio generation on
  compute nodes via Batch Connect `basic` template
- Interact with Meta MusicGen and AudioGen models through a web browser
- Configurable `AUDIOCRAFT_CACHE_DIR` for model download and storage location
- Configurable Slurm account, partition, node type, cores, memory, and GPUs
  via the launch form
- Working directory selector
- Optional additional environment modules can be loaded at launch time
- Multiple CPU and GPU node types supported (AMD Zen3/Zen4, Intel Cascade
  Lake/Skylake, A100, V100)
- Module loaded at runtime: `envs/audiocraft`

## Requirements

### Compute Node Software

- AudioCraft Python environment available as an environment module
  (currently `envs/audiocraft`)
- [Environment Modules](https://modules.readthedocs.io/) with init at
  `/usr/share/Modules/init/bash`
- Python 3 with Gradio, AudioCraft, and their dependencies installed in the
  module environment
- GPU recommended for audio generation workloads

### Open OnDemand

<!-- TODO: Specify the minimum OOD version this app has been tested with -->
- Slurm scheduler

## App Installation

### 1. Clone the repository

```sh
cd /var/www/ood/apps/sys
git clone https://github.com/WFU-HPC/OOD-apps.server.gradio-audiocraft.git
cd OOD-apps.server.gradio-audiocraft
```

### 2. Set up the AudioCraft environment

Make this environment available as an environment module (e.g.,
`envs/audiocraft`), or update `script.sh.erb` to activate it directly.

### 3. Configure for your site

Edit `form.yml.erb` and update these values for your cluster:

| Attribute   | WFU Default            | Change to                          |
|-------------|------------------------|------------------------------------|
| `cluster`   | `"deac"`               | Your cluster name                  |
| `accounts`  | WFU Slurm accounts     | Your Slurm accounts               |
| `queues`    | `"ondemand"`           | Your Slurm partition               |
| `node_type` | WFU-specific node types| Node types on your cluster         |

You will also need to update `submit.yml.erb` if your cluster uses different
Slurm constraint names or node configurations.

In `script.sh.erb`, the app loads the module with:
```
module load envs/audiocraft
```
Ensure an equivalent module is available on your system.

### 4. Verify

No OOD restart is needed (Batch Connect apps are detected automatically).
Visit your OOD dashboard and look for **Gradio AudioCraft** under
**Interactive Apps > Machine Learning and LLMs**.

## Configuration

### form.yml.erb attributes

| Attribute              | Widget          | Description                                   | Default                    |
|------------------------|-----------------|-----------------------------------------------|----------------------------|
| `enable_extra_modules` | check_box       | Toggle extra module loading                   | unchecked                  |
| `extra_modules`        | text_field      | Additional environment modules to load        | `""`                       |
| `working_dir`          | path_selector   | Working directory for the session              | User's `$HOME`             |
| `accounts`             | select          | Slurm account for job submission               | (dynamic from cluster)     |
| `queues`               | select          | Slurm partition                                | `"ondemand"`               |
| `bc_num_hours`         | number          | Maximum wall time (hours)                      | `1`                        |
| `num_cores`            | number_field    | Number of CPU cores                            | `1`                        |
| `memory`               | number_field    | Memory in GB                                   | `8`                        |
| `node_type`            | select          | Compute node type (CPU, GPU, specific HW)      | Any (shortest wait)        |
| `num_gpus`             | number_field    | Number of GPUs (for GPU node types)             | `0`                        |
| `audiocraft_path`      | text_field      | Custom `AUDIOCRAFT_CACHE_DIR` for model storage | `""`                       |
| `enable_audiocraft_path`| check_box      | Toggle custom AudioCraft cache directory        | unchecked                  |

## Troubleshooting

<!-- TODO: Add troubleshooting tips -->

## Testing

<!-- TODO: Update with sites where this app has been deployed -->

| Site                          | OOD Version   | Scheduler | Status |
|-------------------------------|---------------|-----------|--------|
| Wake Forest University (DEAC) | <!-- TODO --> | Slurm     | <!-- TODO --> |

## Known Limitations

<!-- TODO: Document any known limitations -->

## Contributing

Contributions are welcome. To contribute:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/my-improvement`)
3. Submit a pull request with a description of your changes

For bugs or feature requests,
[open an issue](https://github.com/WFU-HPC/OOD-apps.server.gradio-audiocraft/issues).

## References

- [AudioCraft](https://github.com/facebookresearch/audiocraft) -- Meta's
  audio generation framework (MusicGen, AudioGen)
- [AudioCraft MusicGen demo](https://github.com/facebookresearch/audiocraft/blob/main/demos/musicgen_app.py)
  -- the upstream demo script this app is based on
- [Gradio](https://www.gradio.app/) -- the web UI framework used for the
  interface
- [Open OnDemand](https://openondemand.org/) -- the HPC portal framework
- [OOD Batch Connect app development docs](https://osc.github.io/ood-documentation/latest/app-development.html)

### Software Installation

Create a Python environment with the required packages:

```sh
python3 -m venv ${HOME}/env-audiocraft
. ${HOME}/env-audiocraft/bin/activate
python3 -m pip install -r requirements.txt
```

Clone the AudioCraft repository and install audiocraft locally.

```sh
git clone https://github.com/facebookresearch/audiocraft.git
cd audiocraft/
pip install -e .
```

## License

[MIT License](LICENSE)

## Acknowledgments
