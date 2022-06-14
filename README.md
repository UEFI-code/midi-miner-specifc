# Midi Miner Specfic
Python MIDI Specfic track classifier and tonal tension calculation based on spiral array theory

When I forked from the orignal repo, it just check -t "str" is in the input Midi file, and save other type of tracks into the output file.

This one only save your Specficed track!

## installation

### pip
ensure your python version > 3.8:

pip install -r requirements.txt

## Usage
Please refer to the [example notebook](example.ipynb) file for detailed examples.

1. **Total tension calculation**. It will output three tension measures for the midi file. The (tension measures)[https://dorienherremans.com/tension] [3] are based on the spiral array theory by [1], which includes cloud diameter, cloud momentum and tensile strain. The default tension calculation window size is one bar. The tension calculation length window could be set by parameter -w. -w 1 set the window to 1 beat, -w 2 means 2 beat, and -1 is default for a downbeat (1 bar). <br/> **Example:**<br/>tension_calculation.py -i _input_folder_ -o _output_folder_ -k True<br/>
This will run tension_calculation.py on all the file in the _input_folder_ and output the result in 
_output_folder_. -k True means it tries to find key change. Default is not, which is not detecting key change.
It will try to find one key change in the song which is usually in pop songs, but not the classical songs.

The key detection method uses music21 package.


The vertical step in the spiral array theory can be changed by -v parameter, which should be between sqrt(2/15) and sqrt(0.2). The current implementation set it to 0.4.



files_result.json records the file key and potential key changing time and bar position. The output of three tension measures are in pickle format. 

2. **MIDI track separator**. Based on random forest classifier, it can find the melody, bass, chord, and drum tracks in the MIDI file and output a new MIDI file with such tracks, including one potential accompaniment track. Use -t to specify the required tracks, e.g -t "melody bass" will omit the files without both a melody and a bass tracks detected. The default is 'melody'. <br/>  **Example:** <br/> track_separate.py -i _input_folder_ -o _output_folder_  -t "melody bass drum" <br/>
input_folder contains the original midi files, and output_folder is the destination for the new MIDI file. Use -f to select one file.


[1] E. Chew. Mathematical and computational modeling of tonality. AMC, 10:12, 2014.

[2] C. Raffel. "Learning-Based Methods for Comparing Sequences, with Applications to Audio-to-MIDI Alignment and Matching"

[3] D. Herremans & Chew, E. (2016). [Tension ribbons: Quantifying and visualising tonal tension](https://dorienherremans.com/sites/default/files/paper_tenor_dh_preprint_small.pdf). Proc. of the Second International Conference on Technologies for Music Notation and Representation (TENOR). 2:8-18.

## Reference

If you use this libary, please cite the following work: 

Guo R, Simpson I, Magnusson T, Kiefer C., Herremans D..  2020.  A variational autoencoder for music generation controlled by tonal tension. Joint Conference on AI Music Creativity (CSMC + MuMe). 

```
@inproceedings{guo2020variational,
  title={A variational autoencoder for music generation controlled by tonal tension},
  author={Guo, Rui and Simpson, Ivor and Magnusson, Thor and Kiefer, Chris and Herremans, Dorien},
  booktitle={Joint Conference on AI Music Creativity (CSMC + MuMe)},
  year={2020}
}
```

SuperHacker UEFI. https://github.com/UEFI-code/midi-miner-specifc
