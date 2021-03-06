The **2AC** folder contains code and related files for operantly training rodents on a two-alternative choice auditory classification task on an automated plus maze. 

This program shines one of two LEDs (north or south) and waits for response via beam break of associated IR detector. Upon response, an auditory stimulus is played and the East and West LEDs shine and await response via the associated IR detectors. One sound indicates East response and one sound indicates West response. Upon correct response, the associated step motor is moved to produce liquid reward from the syringe pump and the same sound is played again from the response port speaker. Upon incorrect response, an error sound is played.

**Python Files**:   

- 2AC_V03.py (required)  

**Notes**: This program coordinates with each arduino, selects stimulus and initiation ports for each trial, and outputs data into text file.  

**Usage**:``` python 2AC_V02.py --SID 009 --MaxCor 2 --SE B6_triple_1s.wav –SW --C5_single_1s.wav --ProcNum 01```  

**Arguments**:
  - -h, --help 			Show this help message and exit
  - --SID #			    set subject ID: --SID 001
  - --TIP N/S/B     set Trial initiation port: N=North, S-South, B=Both
  - --SpkrLoc #     set speaker location for auditory stims (#1-4)
  - --MaxCor #			set maximum number of consecutive correction trials^: MaxCor 1
  - --SE stimfile		set stimulus for East response port: --SE upsweep.wav
  - --SE stimfile		set stimulus for West response port: --SW upsweep.wav
  - --ProcNum #			set daily procedure number^^: --ProcNum 1

^Correction trials are initiated after error responses. Correction trials result in the same stimulus and same trial initiation port being selected for the next trial. If MaxCor is set to 0, every the stimulus and trial initiation port will be selected randomly.  If MaxCor is set to 2, the same stimulus and trial initiation port will be selected for up to 2 consecutive error responses, after which the stimulus and trial initiation port will be selected randomly again.  

^^Procedure number is set to differentiate files when more than one session is run per day.

- SumData_2AC.py (optional)  

**Notes**: This program analyzes the TrialData.txt output file, providing info on number of trials run, correct/incorrect percentages, turn direction, east/west response biases, and response times.  

**Usage**: ``` python SumData_2AC.py --F 009_2AC_TrialData_012919-01.txt```  

**Arduino Files**
- 2AC_North.ino
- 2AC_East.ino
- 2AC_South.ino
- 2AC_West.ino

**Usage**: Upload each Arduino file to its respective Arduino (e.g., 2AC_East.ino to the East arm response port module).  For the East and West files, set the maxSteps variable (e.g., maxSteps = 2000) to adjust the amount of reward delivery.

