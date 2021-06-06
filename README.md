# EEG-Braking-Intention-with-CNN
## Data Acquisition

This Python project was created to discriminate pre stimulus and pos stimulus signals while driving using EEG signals and a CNN model. Bioelectrical signals were acquired at 250 Hz with g.Nautilus equipment from g.tech, using 30 EEG and 2 EOG channels. Braking and throttle signals were obtained from the OBD port. The dataset was constructed with information of 12 healthy subjects (8 males / 4 females) between 25-38 years that conducted real car driving in a 2.2km test track at a constant speed ranging from 40 to 60km/h for around 45 min. 

## Data Preprocessing
Data pre-processing was carried out in MATLAB using the FieldTrip toolbox.Throttle and brake response times after visual stimulus for all trials for each subject were calculated and it was determined that trials were going to be defined as 3 second intervals, where -1.5 seconds until the visual stimulus (t=0) would be defined as pre-stimulus and from the visual stimulus (t=0) to 1.5 seconds would be defined as post-stimulus. Each test subject had around 120 trials. Trials where the subject failed to detect the visual stimulus or took more than 1.5 seconds to react and trials where break activation before visual stimulus was detected were eliminated to facilitate training of the CNN.

Segmented signals were filtered in a digital pass-band filter from 3-30Hz \cite{c8}. EOG channels were decided to be excluded from the CNN. FP1 and FP2 EEG channels were also eliminated because they were the channels more prone to have movement noise.

In order to prepare the EEG signals for the CNN model, three dimensional matrices for each of the studies were made. Two dimensional matrices for post-stimulus and  pre-stimulus trial segments were made. Channels were loaded into rows and time into columns yielding 28x376 2D matrices per trial segment. Then this matrices were grouped into 3D matrices depending on the study to be carried out resulting in 28x376x2*trials.

## Analysis method
The proposed CNN was done with Python with the Keras library [1], following the architecture proposed by [2]. Three studies were designed in order to test the accuracy of the model:

### Study 1
For the first study, the CNN was trained and tested with the trials of only one test subject. A 10-fold cross validation was performed, where 80\% of the trials were randomly selected for training the CNN and the other 20\% of the trials was used for testing the CNN. This study was repeated for all twelve subjects. 

### Study 2
In the second study, the CNN was trained with all the trials of one subject.The CNN was tested individually with each of the trials of all the twelve subjects (the trials used for training included). This was done for each of the twelve subjects.

### Study 3 
In the third study, the CNN was trained with the trials of all subjects except one subject. The trials of the excluded subject were used for testing the CNN.  This was done for each subject.

## References
[1] Keras (2020) Keras API reference / Keras layers API [ONLINE] Retrieved from:  https://keras.io/api/layers/.

[2] Wang, Z., Yan, W., and Oates, T. (2017, May). Time series classification from scratch with deep neural networks: A strong baseline. In 2017 International joint conference on neural networks (IJCNN) (pp. 1578-1585). IEEE.
