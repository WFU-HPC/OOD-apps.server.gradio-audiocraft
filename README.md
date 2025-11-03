# Gradio AudioCraft App for Open OnDemand (OOD)

Wake Forest University (WFU) HPC Team<br>
Primary Contact: Sean Anderson (anderss@wfu.edu)<br>
`chatbot.py` script created by Cody Stevens

Developed for DEAC OnDemand, the OOD deployment on the DEAC Cluster which is a part of the [WFU HPC Facility](https://hpc.wfu.edu). 


## Description

Create a simple generative-AI music app using Gradio.app as a frontend interface for the AudioCraft framework.


## References

- https://github.com/facebookresearch/audiocraft/blob/main/demos/musicgen_app.py


## Installation


Create a fresh Python environment using any version of Python 3 that you want. Activate the environment after creation:

```sh
python3 -m venv ${HOME}/env-chatbot # create environment
. ${HOME}/env-chatbot/bin/activate  # activate environment
```

Lastly, install the required modules into the environment:

```sh
python3 -m pip install llama_cpp_python gradio openai matplotlib
```
