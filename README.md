# Erwinia-amylovora-virulence-factors-and-prophage-co-evolution
Here, 317 E. amylovora was analyzed, and its virulence factors and their relationships with prophage-related endolysins were assessed. All codes are available in this repository.

# VirulentPred 2.0 Standalone - Ubuntu Environment Setup

This part provides a step-by-step configuration guide and environment setup to run the standalone version of **VirulentPred 2.0** on Ubuntu. 

Since this tool relies on a specific ecosystem of older machine learning and deep learning libraries (such as AutoGluon 0.4.0, PyTorch 1.10, and specific legacy versions of NumPy and Pandas), this guide ensures compatibility by establishing an isolated Python environment.

---

## 1. Download the Original Standalone Tool
Before setting up the environment, download the official VirulentPred 2.0 standalone package from the International Centre for Genetic Engineering and Biotechnology (ICGEB) repository:
* **Official Download Page:** [ICGEB VirulentPred 2.0](https://bioinfo.icgeb.res.in/virulent2/down.html)
* **Direct Download Link:** [virulentpred_2_0.tar.gz](https://bioinfo.icgeb.res.in/virulent2/virulentpred_2_0.tar.gz)

Extract the downloaded archive and navigate into the standalone directory:

```bash
tar -zxvf virulentpred_2_0.tar.gz
cd virulentpred_2_0
```

---

## 2. System-Level Prerequisites

Install the required system development tools, C/C++ compilers, Perl (essential for running the tool's core pipeline), and the necessary libraries required to compile Python from source code:

```bash
sudo apt update
sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python3-openssl git perl
```

---

## 3. Python Version & Virtual Environment Setup

### Step A: Install pyenv and Python 3.9.11

1. Install `pyenv` using the official automatic installer script:

```bash
curl https://pyenv.run | bash
```

2. Configure your shell environment by appending the following lines to your `~/.bashrc` file to ensure `pyenv` loads automatically, then reload the shell:

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
exec $SHELL
```

3. Compile and install Python 3.9.11 (this building process might take a few minutes):

```bash
pyenv install 3.9.11
```

### Step B: Create and Activate the Isolated Environment

While inside your extracted `virulentpred_2_0` directory, generate and trigger the virtual environment using the freshly installed Python 3.9.11:

```bash
# Create the virtual environment named 'venv'
~/.pyenv/versions/3.9.11/bin/python -m venv venv

# Activate the virtual environment
source venv/bin/activate
```

*(Once activated, you should see a `(venv)` prefix appended to your terminal prompt).*

---

## 4. Install Dependencies

To prevent dependency version mismatches, ensure your virtual environment remains **active**, then run these installation commands sequentially:

```bash
# Upgrade core packaging tools inside the environment
pip install -U pip setuptools wheel

# Install PyTorch (CPU-only stable build required by this framework)
pip install torch==1.10.1+cpu -f https://download.pytorch.org/whl/cpu/torch_stable.html

# Install the exact verified dependency stack from requirements.txt
pip install -r requirements.txt
```

---

## 5. Running the Prediction

After a successful installation sequence, verify the deployment by running the core script against the provided sample protein sequence file:

```bash
perl predict.pl sample_seq.fas
```

*Note: The PSSM (Position-Specific Scoring Matrix) profile calculation step is computationally heavy. Depending on your virtual machine or hardware specifications, the prompt may seem paused; please allow sufficient time for completion.*

---

## Troubleshooting

If you encounter any issues during setup or execution, please ensure:
- All system-level prerequisites are installed correctly
- The virtual environment is properly activated before installing dependencies
- You are using Python 3.9.11 as specified
- The required versions of dependencies match those in `requirements.txt`

For additional support, refer to the official VirulentPred 2.0 documentation or contact the ICGEB support team.

