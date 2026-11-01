Parentage index (likelihood-based)
When two or three sires all pass a Mendelian check, you still have to decide which one is the father. This script is for that situation.
Instead of just counting conflicts, it asks how much more likely the genotypes are if a candidate is the parent than if he is a random, unrelated animal. The evidence from every SNP is added up into a single parentage index (PI), and candidates are ranked by it.
What you get
For each candidate: the PI (also as log10), the number of Mendelian conflicts, a final call (Supported, Not supported or Indeterminate) and an estimated probability that this candidate is the parent. That probability only compares candidates that survive the conflict filter, and it leaves room for the real parent not being in your list at all, which happens more than you'd like.
A few choices I made on purpose
Allele frequencies never include the animals being tested. Otherwise the offspring and its parents would be helping to prove their own relationship.
Genotyping error is built into the model, so one bad SNP doesn't sink a true parent.
Optional QC on autosomes, minor allele frequency and SNP spacing, to keep correlated markers from inflating the evidence.
Using it
```bash
python parentage_pi.py --raw parentage.raw --offspring ID_OFFSPRING \
    --parent ID_SIRE1 ID_SIRE2 --freq reference.frq --bim parentage.bim
```
Input is a PLINK `.raw` file plus allele frequencies from a reference population (a `.frq` file, or a list of reference animals). Output is a CSV ranked by evidence.
Keep in mind
Run sires and dams separately, since it assumes one true parent per run. The result is only as good as the reference population behind the allele frequencies.
Part of the SelectaGen toolkit. The code is private; reach out if you want to test it on your own data.
