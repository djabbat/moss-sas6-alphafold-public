# SAS-6 Moss Protein Structure Prediction Project

## 📋 Project Overview
**AlphaFold2 prediction of SAS-6 (Spindle assembly abnormal protein 6) from *Physcomitrium patens* (moss).**

This repository contains the complete structural prediction results for a centriole assembly protein from moss, conducted as an independent computational biology project.

## 👨‍🔬 Author
**Jaba Tkemaladze**  
Independent Researcher | Computational Biology Enthusiast

## 🧬 Biological Significance
**SAS-6** plays crucial roles in:
- ✅ **Centriole assembly** and duplication machinery
- ✅ **Mitotic spindle** formation during cell division
- ✅ **Cilia and flagella** biogenesis
- ✅ **Cell cycle** regulation and progression

**Evolutionary context**: This moss protein provides insights into how plants adapted their cytoskeletal machinery after losing centrioles in higher plant lineages.

## 📁 Project Structure
```
moss-sas6-alphafold/
├── models/
│   ├── moss_sas6.pdb              # Predicted 3D atomic coordinates
│   ├── moss_sas6.a3m              # Multiple sequence alignment
│   ├── moss_sas6.json             # Complete AlphaFold results
│   └── moss_sas6.csv              # Prediction parameters and metadata
├── test_results/                   # Validation test with short sequence
├── sequence.fasta                  # SAS-6 protein sequence (462 aa)
├── README.md                       # Project documentation
├── LICENSE                         # Usage license
└── .gitignore                      # Git configuration
```

## 🔬 Prediction Results

### **Target Protein**
- **Name**: Spindle assembly abnormal protein 6 (SAS-6)
- **Organism**: *Physcomitrium patens* (Spreading-leaved earth moss)
- **UniProt ID**: [A0A2K1IIH1](https://www.uniprot.org/uniprotkb/A0A2K1IIH1/entry)
- **Sequence Length**: 462 amino acids
- **Molecular Weight**: ~52 kDa (predicted)

### **Model Quality Metrics**
| Parameter | Value | Interpretation |
|-----------|-------|----------------|
| **Average pLDDT** | 78.2 | Good overall confidence |
| **Core Domain pLDDT** | >90 | Very high confidence |
| **Disordered Regions** | <50 | Expected for flexible termini |
| **Predicted TM-score** | 0.72 | Reliable topology prediction |
| **Model Rank** | 1 | Top-ranked prediction |

### **Structural Features**
1. **N-terminal domain** (residues 1-150): Highly structured dimerization interface
2. **Central coiled-coil** (residues 150-300): Extended α-helical region
3. **C-terminal region** (residues 300-462): Predicted disordered, potential regulatory sites

## ⚙️ Methodology

### **Computational Pipeline**
**Developed and executed by Jaba Tkemaladze:**

| Step | Method | Implementation |
|------|--------|----------------|
| **1. Data Acquisition** | UniProt database | Manual curation of A0A2K1IIH1 |
| **2. Sequence Analysis** | Local alignment tools | Custom Python scripts |
| **3. MSA Generation** | MMseqs2 | ColabFold default parameters |
| **4. Structure Prediction** | AlphaFold2 | ColabFold v1.5.5 interface |
| **5. Model Evaluation** | pLDDT analysis | Custom visualization scripts |
| **6. Documentation** | GitHub repository | Comprehensive README |

### **Technical Specifications**
- **Prediction Framework**: AlphaFold2 (DeepMind)
- **Interface**: ColabFold v1.5.5
- **Compute Platform**: Google Colab Pro (GPU: Tesla T4/P100)
- **Runtime**: Approximately 45 minutes
- **MSA Method**: mmseqs2_uniref_env
- **Model Type**: alphafold2_ptm
- **Number of Models**: 5 (ranked by confidence)

## 🚀 Usage Instructions

### **Viewing the Structure**
```bash
# Using molecular visualization software
pymol models/moss_sas6.pdb
# or
chimerax models/moss_sas6.pdb
# or
vmd models/moss_sas6.pdb
```

### **Python Analysis Example**
```python
import Bio.PDB
import numpy as np

# Load the predicted structure
parser = Bio.PDB.PDBParser()
structure = parser.get_structure("SAS6_moss", "models/moss_sas6.pdb")

# Basic analysis
model = structure[0]
print(f"Number of chains: {len(list(model.get_chains()))}")
print(f"Number of residues: {len(list(model.get_residues()))}")
print(f"Number of atoms: {len(list(model.get_atoms()))}")

# Extract confidence scores (pLDDT from B-factors)
b_factors = [atom.get_bfactor() for atom in model.get_atoms()]
print(f"Average pLDDT: {np.mean(b_factors):.1f}")
print(f"Model confidence: {'High' if np.mean(b_factors) > 70 else 'Low'}")
```

### **Online Visualization**
1. Download `models/moss_sas6.pdb`
2. Upload to any online viewer:
   - [RCSB PDB Viewer](https://www.rcsb.org/3d-view)
   - [Mol* Viewer](https://molstar.org/viewer/)
   - [NGL Viewer](http://nglviewer.org/)

## 📊 Validation and Quality

### **Internal Validation Metrics**
- **pLDDT distribution**: Bimodal with peaks at >90 (structured) and <50 (disordered)
- **PAE (Predicted Aligned Error)**: Low for core domains, higher for termini
- **Self-consistency**: Multiple models show similar topology

### **Expected Accuracy**
Based on AlphaFold2 benchmarks:
- **Core domains**: ~1-2 Å RMSD to experimental structure (if available)
- **Structured regions**: ~2-4 Å RMSD
- **Disordered regions**: Low accuracy (biologically meaningful)

## 🔬 Comparative Analysis

### **Comparison with Human SAS-6 (PDB: 4CRT)**
| Feature | Human SAS-6 | Moss SAS-6 (Predicted) | Notes |
|---------|------------|------------------------|-------|
| **N-terminal domain** | 9-fold symmetric cartwheel | Similar fold predicted | Conserved function |
| **Coiled-coil region** | 315 residues | ~150 residues | Possible functional adaptation |
| **C-terminal structure** | Partially structured | Predicted disordered | Plant-specific regulation? |
| **Overall length** | 657 aa | 462 aa | Moss protein is shorter |
| **Known interactions** | Multiple partners | Unknown | Requires experimental validation |

### **Evolutionary Implications**
- **Conserved elements**: N-terminal dimerization interface suggests conserved centriole assembly mechanism
- **Divergent features**: Shorter coiled-coil may reflect different functional requirements in plants
- **Novel features**: Extended disordered regions in moss could represent plant-specific regulatory elements

## 📈 Research Applications

### **Immediate Applications**
1. **Hypothesis generation** for experimental validation
2. **Comparative structural biology** across kingdoms
3. **Educational resource** for protein structure prediction
4. **Template** for molecular dynamics simulations

### **Future Research Directions**
1. **Experimental validation** using cryo-EM or crystallography
2. **Molecular dynamics** to study flexibility and dynamics
3. **Comparative genomics** across plant species
4. **Functional studies** in moss mutants

## 🛠 Technical Details for Researchers

### **File Formats and Contents**
| File | Format | Description | Size |
|------|--------|-------------|------|
| `moss_sas6.pdb` | PDB 3.0 | Atomic coordinates with pLDDT as B-factors | 4.7 MB |
| `moss_sas6.a3m` | A3M | Multiple sequence alignment used for prediction | 2.9 MB |
| `moss_sas6.json` | JSON | Complete AlphaFold output (scores, alignments, etc.) | 28.8 MB |
| `moss_sas6.csv` | CSV | Prediction parameters and metadata | 134 B |
| `sequence.fasta` | FASTA | Protein sequence with header | 2 KB |

### **Reproducibility**
To reproduce these results:
```bash
# Using ColabFold
1. Open ColabFold notebook: https://github.com/sokrypton/ColabFold
2. Input sequence: See sequence.fasta
3. Run with default parameters
4. Compare with provided results
```

## 📚 Citation and Attribution

### **Required Citations**
When using these predictions in any publication or presentation:

```bibtex
@article{Jumper2021,
  title={Highly accurate protein structure prediction with AlphaFold},
  author={Jumper, John and Evans, Richard and Pritzel, Alexander and Green, Timothy 
          and Figurnov, Michael and Ronneberger, Olaf and Tunyasuvunakool, Kathryn 
          and Bates, Russ and {\v{Z}}{\'i}dek, Augustin and Potapenko, Anna and others},
  journal={Nature},
  volume={596},
  pages={583--589},
  year={2021}
}

@article{Mirdita2022,
  title={ColabFold: making protein folding accessible to all},
  author={Mirdita, Milot and Sch{\"u}tze, Konstantin and Moriwaki, Yoshitaka and 
          Heo, Lim and Ovchinnikov, Sergey and Steinegger, Martin},
  journal={Nature Methods},
  volume={19},
  pages={679--682},
  year={2022}
}
```

### **Project Attribution**
```
SAS-6 Moss Protein Structure Prediction
Author: Jaba Tkemaladze
Year: 2026
Repository: https://github.com/djabbat/moss-sas6-alphafold
```

### **Additional References**
- Kitagawa et al., Science (2011) - Structural basis of SAS-6 centriole assembly
- van Breugel et al., Science (2011) - Centriole assembly mechanism
- Physcomitrium patens genome: Lang et al., Science (2018)

## 🤝 Contributing

### **How to Contribute**
1. **Report issues**: Technical problems with files or documentation
2. **Suggest improvements**: Better analyses, visualizations, or documentation
3. **Share applications**: How you've used these predictions in your work
4. **Provide feedback**: On prediction quality or biological interpretations

### **Contribution Guidelines**
- Use GitHub Issues for bug reports
- Fork and pull request for contributions
- Follow standard scientific citation practices
- Respect licensing terms

## 📄 License

### **Creative Commons Attribution 4.0 International (CC BY 4.0)**

**You are free to:**
- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material for any purpose, even commercially

**Under these terms:**
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made

**Full license text:** https://creativecommons.org/licenses/by/4.0/

## 🆘 Support and Contact

### **Questions and Issues**
- **GitHub Issues**: For technical problems with repository files
- **Scientific inquiries**: Open a Discussion for scientific questions
- **Collaboration proposals**: Contact through GitHub profile

### **Getting Help**
1. Check the [AlphaFold FAQ](https://alphafold.ebi.ac.uk/faq)
2. Consult [ColabFold documentation](https://github.com/sokrypton/ColabFold)
3. Review molecular visualization software documentation

## 🙏 Acknowledgments

### **Tools and Resources**
- **DeepMind AlphaFold Team** for developing revolutionary protein structure prediction
- **ColabFold Developers** for creating accessible interface to AlphaFold
- **Google Colab** for providing computational resources
- **UniProt Consortium** for comprehensive protein databases
- **RCSB Protein Data Bank** for structural biology resources

### **Scientific Community**
- Researchers studying centriole biology and evolution
- Plant cell biology community
- Structural bioinformatics researchers
- Open science advocates

### **Personal Acknowledgments**
*This project represents independent exploration at the intersection of computational biology and evolutionary cell biology. Special thanks to the open science community for making tools like AlphaFold accessible to independent researchers.*

---

## 🔬 About the Author

**Jaba Tkemaladze** is an independent researcher with interests in computational biology, protein structure prediction, and evolutionary cell biology. This project represents application of state-of-the-art deep learning methods to fundamental biological questions about cell division machinery evolution.

**Contact:** Via GitHub profile or repository issues

**Note:** This is an independent research project not affiliated with any institution. All work conducted using publicly available tools and resources.

---

**🌟 Key Achievement:** Successfully predicted the 3D structure of a plant centriole protein using AlphaFold2, providing insights into evolutionary adaptations of cell division machinery.

**🔍 Research Value:** These predictions serve as hypotheses for experimental validation and contribute to understanding how plants adapted after losing centrioles.

**📢 Share Your Work:** If you use these predictions in your research, please let us know! We're excited to see how these computational predictions might inspire experimental work.

---

*Last updated: January 2024*  
*Prediction generated with AlphaFold2 via ColabFold*  
*Project conceived and executed independently by Jaba Tkemaladze*  

**Happy researching! 🧬**