# Compact virtual realilty setup for neuroimaging

We study neural activity in the mouse hippocampus in virtual reality using various optical techniques, including voltage imaging, calcium imaging and optogenetic modulation.

Here we share the hardware &amp; software we developed for the behavioral setup.

<img src="https://user-images.githubusercontent.com/98536980/168963574-b6dd15a1-4110-4217-9a43-964b31d9217e.jpg" width="685" height="454" align="center">

## 3D printings
 
 We based our wheel design on [Arthur Sugden](https://github.com/asugden/bebox/tree/master/3d/wheel) model with slight changes.
 
 Our models can be found in [`3D models`](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/tree/main/3D%20models) directory which contains models for:
 
 - The wheel
 - U shape base for the wheel axis
 - Holders and axle
 - Screen for VR projection

Have a look [here](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/blob/main/3D%20models/Assembly.STL) on the assembled model.
 
 
## Electronics & more

- [Capacitance sensor](https://www.sparkfun.com/products/12041) - for lick detections.
- [Solenoid valve](https://theleedifference.com/products/#solenoid-valves/3) - for reward control.
- [H bridge](https://m.banggood.com/10-Pcs-Geekcreit-L298N-Dual-H-Bridge-Stepper-Motor-Driver-Board-p-1054211.html?utm_source=googleshopping&utm_source=googleshopping&utm_medium=cpc_organic&utm_medium=cpc_bgs&gmcCountry=IL&utm_content=minha&utm_content=sandra&utm_campaign=minha-il-en-mb&utm_campaign=sandra-ssc-il-all-0507&currency=ILS&cur_warehouse=CN&createTmp=1&ad_id=519822680399&gclid=Cj0KCQiA6NOPBhCPARIsAHAy2zBwOR6kqKPrn7NYVQt2XXXowL66YlR-dfJfsxjh51QuHRhCAJZCJ7saAtPREALw_wcB) - for 12V voltage supply for the valve.
- [Rotary encoder](https://www.ia.omron.com/data_pdf/cat/e6b2-c_ds_e_6_1_csm491.pdf?id=487) - for wheel spinning detection.
- [Arduino Uno](https://docs.arduino.cc/hardware/uno-rev3) - controlling the electrical devices.
- [LED projector](https://www.optoma.com/ap/product/ml750st/#) - project the VR environment in front of the mice.
- [500 nm shortpass filter](https://www.edmundoptics.com/p/500nm-50mm-diameter-od-4-shortpass-filter/27788/) - prevent interference of light from the projector with fluorescence detection. 
- [Bearings](https://www.4project.co.il/product/flanged-ball-bearing-5x14x5).

### Motorized control setup

Our setup can use either for freely running mice experiment or for motorized controled locomotion experiment. Motorzied control will need the following: 

- [Motor](https://www.pololu.com/product/2207)
- [Motor controller](https://www.pololu.com/product/1376)


## Hardware all together

 We based the Wheel on [ThorLabs Breadboard](https://www.thorlabs.com/newgrouppage9.cfm?objectgroup_id=159) with ThorLabs standart posts and connectors.

### Mouse head fixation

 The mice head was fixed by [Neurotar head fixation system](https://www.neurotar.com/the-mobile-homecage/#stability).
 
<img src="https://user-images.githubusercontent.com/98536980/152039318-e970ad76-c7f7-4bf8-936f-f8c45221edb3.jpeg" width="300" height="350">

### Reward delivery and lick detection

Tube (filled with 10% sucrose water for reward delivery), was connected to [Neurotar lick port](https://www.neurotar.com/the-mobile-homecage/#stability) from one end, and to solenoid valve from the other end. The solenoid valve was connected to an H-bridge for voltage supply. An electrical wire was soldered to the edge of a needle which compose on the lick port. This wire was connected to a capacitance sensor for mouse lick detection.

<img src="https://user-images.githubusercontent.com/98536980/152039358-6db3975e-dfc3-45fc-8f1e-7cf7f580c015.jpeg" width="300" height="350">

Depend on the experimental setup - we used a motor for motorized control experiment or rotary encoder for freely running experiment:

### Motorized control

The motor was placed on the shaft and is being controlled by [Pololu control center](https://www.pololu.com/docs/0J44/3.1).

<img src="https://user-images.githubusercontent.com/98536980/172154398-65e1c0f4-df8a-4a1f-861c-d0249964dc25.jpg" width="300" height="350">

### Rotary encoder

 A rotary encoder was fixed on the shaft of the wheel to track the wheel rotation
  
<img src="https://user-images.githubusercontent.com/98536980/152039393-15f94a31-0364-4099-9c3a-60a78214d7ac.jpeg" width="300" height="350">

### Arduino control

The H-bridge, capacitance sensor and the rotary encoder were connected to an arduino uno. The arduino was connected to a standard computer, installed with the ViRMen environment. 

<img src="https://user-images.githubusercontent.com/98536980/152808787-f24bdea9-071d-4f8d-a9d5-d9a4fee9c81d.png" width="300" height="350">

Have a look [here](https://www.circuito.io/app?components=9442,10456,11021,11696,44752,860025) for interactive circutry design.

### The projector

The projector was mount on the ThorLabs breadboard to project the VR environment on 3D printed screen that was placed in front of the wheel.
 
<img src="https://user-images.githubusercontent.com/98536980/152039487-7858f3c2-c7bf-4502-821c-9ef62dac772b.jpeg" width="400" height="250">
 
## Software

The VR rendering designed and executed by [ViRMEn v.2016-02-12](http://pni.princeton.edu/pni-software-tools/virmen-download).
Configurations files for 3 different VR worlds can be found at [`ViRmEn\Mice_Training.mat`](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/tree/main/ViRmEn).

This what the mouse is seeing on the wheel:

<img src="https://user-images.githubusercontent.com/98536980/172183034-699b71a5-069e-4b6c-8489-99bb154f00d6.gif" width="450" height="300" align="center">

Beside the VR design we had to control on the following:
- Progress of the VR according to the mice movement on the wheel
- Release specific amount of reward (i.e. sucrose water) at a specified location (i.e. reward zone)
- keep track of the mouse licking (for learning progress analysis)
- Save the behavioral data from the training and Imaging sessions for future analysis

The [arduino code](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/blob/main/Arduino/wheel_control.ino) used for hardware control. Each 10 ms it send data to virmen via serial port communication to indicate if lick oocured and the amount of spinning of the wheel.
Virmen will also send data to the arduino via the same serial port, to indicate when to open the valve for reward delivery.
We also supply compiled arduino files for automatic initialization of the arduino board from the virmen script.

The software allows flexible training logic based on the mouse progress. In the beginning of each training session, the trainer need to declare the current training stage:

<img src="https://user-images.githubusercontent.com/98536980/152346139-fcaaa5a1-cf53-491e-b12b-43afecabe5d1.jpeg" width="120" height="150">

Then, the mouse meta-data should be given:

<img src="https://user-images.githubusercontent.com/98536980/152346599-a7af7c9b-0426-423c-9dd2-fcf7cce3f366.jpeg" width="120" height="150">

Now the training begin and we can track the mouse preformance:

<img src="https://user-images.githubusercontent.com/98536980/152347088-6d8f3362-81f3-4c35-bcaa-c08bd8368aa9.jpeg" width="500" height="400">

The virmen experiment and moveforward code can be found at [`ViRmEn`](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/tree/main/ViRmEn) directory.
After the training finished the mouse training data was saved as a csv.file and automated python script is running to preform analytics of the current training session. The script send summary data to the lab members emails with the curnet day data, including plots about the training history of the mouse:

<img src="https://user-images.githubusercontent.com/98536980/152347980-54f78c41-0e4e-4b14-9f4c-53d236ccaf72.png" width="400" height="300" align="center">

Have a look at the [daily summary plots](https://github.com/yoavadamlab/VR-setup/files/7994692/daily_plots.2.pdf).

The code for the behavioral analysis can be found in the [`Behavior Analysis`](https://github.com/yoavadamlab/VR-setup-for-NeuroImaging/blob/main/Behavior%20Analysis/Mice_training_data_analysis_wheel_setting.py) directory.

## Contact us

For more information and quetsions you are welcome to contact us by openning an issue.

## Contributors
Project was led by [Yaniv Melamed](https://elsc.huji.ac.il/lab-members/yaniv-melamed/) in collaboration with [Rotem Kipper](https://elsc.huji.ac.il/lab-members/rottem-kipper/) and advice from all [Adam Lab members](https://elsc.huji.ac.il/people-directory/faculty-members/yoav-adam/). 3D priniting was provided by [ELSC FabLab](https://elsc.huji.ac.il/research-and-facilities/expertise-centers/elsc-fablab/).
