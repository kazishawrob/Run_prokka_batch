# Prokka Genome Annotation Script

This Bash script automates the annotation of multiple `.fna` genome files using [Prokka](https://github.com/tseemann/prokka). Each genome file is processed individually, and results are stored in a structured output directory.

## Features
- Loops through all `.fna` or .fasta'files in the current directory. change the `.fna` to `.fasta ` Creates an organized output directory (`Prokka_Results`).
- Generates separate result folders for each genome file.
- Uses the `--force` option to overwrite existing directories if needed.

## Prerequisites
Ensure you have **Prokka** installed. You can install it via:
```bash
conda install -c bioconda prokka
```

## Usage
1. Place your `.fna` files in the working directory.
2. Save the script as `run_prokka.sh`.
3. Give the script execution permission:
   ```bash
   chmod +x run_prokka.sh
   ```
4. Run the script:
   ```bash
   ./run_prokka.sh
   ```

## Script Details
```bash
#!/bin/bash

# Directory to store Prokka outputs
output_directory="./Prokka_Results"

# Create the output directory if it doesn't exist
mkdir -p "$output_directory"

# Loop over each .fna file in the current directory
for fna_file in *.fna; do
  # Get the base name of the file (without path and extension)
  base_name=$(basename "$fna_file" .fna)
  # Create an output folder named after the base name
  output_folder="$output_directory/$base_name"
  mkdir -p "$output_folder"
  
  # Run Prokka with the --force option to overwrite existing directories
  prokka --outdir "$output_folder" --prefix "$base_name" --force "$fna_file"
done
```

## Output
Each `.fna` file generates an annotated output in:
```
Prokka_Results/
  ├── sample1/
  │   ├── sample1.gff
  │   ├── sample1.faa
  │   ├── sample1.ffn
  │   ├── sample1.tsv
  │   ├── ...
  ├── sample2/
  ├── ...
```

## License
This project is open-source. Feel free to use and modify as needed.

## Contributions
Contributions are welcome! Feel free to fork the repository and submit a pull request.

