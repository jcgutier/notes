


# Remove password on PDF

To remove the password on a PDF with the GUI, follow:

- Open the file and decrypt it
- Press `strl +p` to print it and save it as a PDF

To remove the password on a PDF with the CLI, run:

```bash
# qpdf is pre-installed on some distributions
qpdf --password=<your-password> --decrypt /path/to/secured.pdf out.pdf
# Or with pdftk, but this need to be installed first
pdftk /path/to/input.pdf input_pw <yourpassword> output out.pdf
```
