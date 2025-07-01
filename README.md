# Tutorial: Setting up and Running CORASON on Windows Subsystem for Linux (WSL)

This guide walks you through installing Miniconda, setting up the CORASON environment, running an example, and viewing the output.

## Prerequisites

- Windows 10 or 11
- [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/) enabled and installed (Ubuntu recommended)

---

## Step 1: Launch WSL

Open your WSL terminal (Ubuntu):

```bash
wsl
```

Update packages:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2: Install Miniconda

Download the Miniconda installer:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Run the installer:

```bash
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the prompts (accept license, choose install location, allow to initialize Conda).

Close and reopen the terminal or activate conda:

```bash
source ~/.bashrc
```

---

## Step 3: Clone the CORASON Repository

Install `git` if not already available:

```bash
sudo apt install git -y
```

Clone the repository:

```bash
git clone https://github.com/nselem/CORASON.git
cd CORASON
```

---

## Step 4: Create the Conda Environment

Create the environment using the provided `.yml` file:

```bash
conda env create -f environment.yml
```

Activate the environment:

```bash
conda activate corason
```

---

## Step 5: Uncompress the Example Dataset

Inside the CORASON folder:

```bash
unzip EXAMPLE.zip -d example_data
cd example_data
```

---

## Step 6: Run CORASON

Once in the example directory, execute CORASON with a typical command like:

```bash
corason.pl -r reference.gbk -q tauD -d genome_database_folder
```

Make sure the `.gbk` files and query are correctly specified as in the example.

---

## Step 7: View the Output

CORASON will generate several outputs including:

- `Joined.svg`: A scalable vector graphic of gene cluster relationships and phylogenies.

### To open `Joined.svg`:

From Windows, navigate to the path of your WSL home directory (e.g., `\\wsl$\Ubuntu\home\your-user\...`) and open `Joined.svg` with your preferred browser.

Alternatively, copy to Windows:

```bash
cp Joined.svg /mnt/c/Users/YourName/Desktop/
```

---

## Tips

- Make sure to activate your `corason` environment every time before running.
- Use `conda deactivate` to exit the environment.
- You can install additional tools or dependencies via `conda install` as needed.

---

## References

- CORASON: https://github.com/nselem/CORASON
- BiG-SCAPE/CORASON publication: https://doi.org/10.1038/s41589-019-0400-9
