# Molecule-RNN
Molecule-RNN is a recurrent neural network built with Pytorch to generate molecules for drug discovery. It is trained with the [Zinc](https://zinc.docking.org/) dataset. The [SELFIES](https://github.com/aspuru-guzik-group/selfies) is used as the representation of molecules. The SMILES files are converted to SELFIES during training on-the-fly.

## Training
1. Dowdload the SMILES files of molecules from [Zinc](https://zinc.docking.org/). Select "SMILES(*.smi)" and "Flat" opitions when downloading.

2. Modify the path of dataset in ```train.yaml``` to your downloaded dataset by setting the value of ```dataset_dir```.

3. Run the training script.
```
python train.py
```

## Sampling
We can generate molecules by sampling the model according to the output distribution. 
```
python sample.py
```
The sampled output is in the format of SELFIES:
```
[C][C][\N+expl][=N][SnH2+expl][=S@expl][Oexpl][P@Hexpl][PHexpl][S@expl][C][C][I][C@@expl][\C@@expl][P@@Hexpl][\Oexpl][\N+expl][Nexpl][N+expl][Expl\Ring2][=I][=P@Hexpl[=O+expl][C][Expl=Ring1][=P@Hexpl][CH2expl][\F][/S@expl][=Siexpl][Sn+3expl][N+expl][/S@expl][O][BH3-expl][Expl/Ring1][Oexpl][S@Hexpl]
```
The advantage of SELFIES is that the output is always a valid molecule. Note that the SELFIES is an [automata](https://en.wikipedia.org/wiki/Automata_theory), and it terminates when there is no chemical bonds to build. So the converted SMILES could be shorter than the SELFIES:
```
CC\[N+]=N[SnH2+]=[S@][O][P@H][PH][S@]CCI
```
<p align="center">
<img width="250" height="100" src="figure/sampled_mol.png">
</p>   

