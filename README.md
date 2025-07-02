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
chmod +x Miniconda3-latest-Linux-x86_64.sh
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
git clone https://github.com/miguel-mx/corason-conda.git
cd CORASON
```

---

## Step 4: Create the Conda Environment

Create the environment using the provided `.yml` file:

```bash
conda env create -f corason.yml
```

Activate the environment:

```bash
conda activate corason
```

Install aditional dependencies
```bash
cpanm SVG
```
---

## Step 5: Uncompress the Example Dataset

Inside the corason-conda folder:

```bash
tar xvfz EXAMPLE.tar.gz
cd EXAMPLE
```

---

## Step 6: Run CORASON

Once in the example directory, execute CORASON with a typical command like:

```bash
 ../CORASON/corason.pl -q ctg2_515.query -rast_ids Example.Ids -s 501926

```

### What Each Argument Means:

- `../CORASON/corason.pl`  
  This is the main CORASON Perl script. Make sure you're running it from within the `EXAMPLE` folder so the relative path to the script is correct.

- `-q ctg2_515.query`  
  This is your **query file**, in FASTA format. It represents a gene (or genes) from a specific **contig** that you are interested in.  
  🧬 To select a contig, you should:
  1. Open the `.gbk` file for genome `501926` using a genome viewer or text editor.
  2. Identify the contig that contains your gene of interest.
  3. Extract the sequence of that contig and save it in FASTA format as `ctgX.query`.

- `-rast_ids Example.Ids`  
  This is a list of genome IDs (e.g., GenBank files) that you want CORASON to search through. It acts as an index of available `.gbk` files and must match the filenames or internal IDs of the genome database.

- `-s 501926`  
  This specifies the **source genome** for the query. It tells CORASON which `.gbk` file contains the contig specified in the `-q` parameter.

---

### ✅ Important: Run the Command from Inside the `EXAMPLE` Folder

To ensure all relative paths resolve correctly, run the command from within the `EXAMPLE` directory (or wherever your data and `.Ids` file are located):

```bash
../CORASON/corason.pl -q ctg2_515.query -rast_ids Example.Ids -s 501926
```

---

## Step 7: View the Output

CORASON will generate several outputs including:

- `Joined.svg`: A scalable vector graphic of gene cluster relationships and phylogenies.

### To open `Joined.svg`:

From Windows, navigate to the path of your WSL home directory.
(e.g., `\\wsl$\Ubuntu\home\your-user\corason-conda\EXAMPLE\output\ctg2_515.query-output\`) 
and open `Joined.svg` with your preferred browser.

Also, you can open the Windows **File Explorer** and look for your WSL, and go to 
`/home/<user>/corason-conda/EXAMPLE/output/ctg2_515.query-output/` 
There you can open `Joined.svg`. 

## Example Output

Below is an example of a CORASON output:

![CORASON output preview](Joined.png)


---

## Tips

- Make sure to activate your `corason` environment every time before running.
- Use `conda deactivate` to exit the environment.
- You can install additional tools or dependencies via `conda install` as needed.

---

## References

- CORASON: https://github.com/nselem/corason
- BiG-SCAPE/CORASON publication: https://doi.org/10.1038/s41589-019-0400-9
- CORASON-Conda: https://github.com/miguel-mx/corason-conda
