# deep-vs
In this study, the aim is to estimate the most suitable ligand for protein binding using the description vectors of the cavities of the proteins.

The data used while training the model was obtained from PDBbind that contains proteins and ligands in docked conformation. The cavities on the proteins were generated by using the IChem toolkit while the ligands were embedded using an unsupervised model that is called Mol2vec. Once both the data on cavities and ligands were generated, the deep neural network was constructed to ultimately find a ligand that would bind to the given cavity.    
Eventually, the model has successfully predicted molecular structures that were very similar to already known molecules that reside in the specified cavity with 91\% accuracy. 

## Requirements
- [keras](https://keras.io/)
- [tensorflow](https://www.tensorflow.org/) 
- [pandas](http://pandas.pydata.org/)
- [NumPy](http://www.numpy.org/)
- [scikit-learn](http://scikit-learn.org/stable/)
- argparse


Note that Python version is 3.7.4.

## Installation
`git clone https://github.com/bsa-vsp/deep-vs.git`

`cd deep-vs`

`pip install -r requirements.txt`

Download [IChem](http://bioinfo-pharma.u-strasbg.fr/labwebsite/download.html)

## Usage

In order to use the model, you need to obtain the description vectors of the cavities of the protein you are interested in via IChem.

You can see how the resulting cavity file should be in the example cavity vector file.

Once you have the cavity vector file, you can use it as input.

 `python mlp_vscreen_predict.py -i cavitiy_vectors.csv -m mlp_vscreen_train_model.h5 -o predicted_lig.csv`
 
The model will predict the most suitable ligand vectors for your cavities. 

You can find the SMILES of the ligand that is the most similar to the predicted ligand vector by screening from the [eMolecules](https://www.emolecules.com/) library containing 100 thousand diverse molecules. The size of this library exceeds the github upload limit, but you can download the library via this [link](https://drive.google.com/drive/folders/1OMdrh4el6OYd2-7idg4Dg6quBix6_cDp?usp=sharing).

*Also if you want, you can establish a library that is bigger or contains more diverse molecules in order to improve similarity of output. Please note that the output of the model is in the Mol2vec output format, so you need to convert the library you created into the vector with [Mol2vec](https://github.com/samoturk/mol2vec).*
 
 `python mlp_vscreen_library.py -i predicted_lig.csv -l 100k.csv`

## Example:

If you want to try it, you can use the cavity file of 2le3 protein obtained with Ichem which is 2le3_cavitiy_vectors.csv, and the eMolecules library containing 10 thousand molecules which is 10k.tar.xz. 

`python mlp_vscreen_predict.py -i 2le3_cavitiy_vectors.csv -m mlp_vscreen_train_model.h5 -o 2le3_predicted_lig.csv`

`tar -xf 10k.tar.xz | python mlp_vscreen_library.py -i 2le3_predicted_lig.csv -l 10k.csv`
