
# UFF-SCIFI-Datasets
Access Points (AP) Utilization Datasets from UFF SCIFI wireless network

# What Is the SCIFI Network

UFF SCIFI wireless network is a large-scale wireless developed by Fluminense Federal University, financed by RNP (Brazilian National Research and Education Network). It was developed to be a low-cost open-source option to the deployment, configuration, operation and management of large-scale wireless network. The SCIFI network is composed of a smart controller, also named SCIFI controller, and low cost APs, operating under the open source OpenWRT firmware.  SCIFI controller is a central management unit and monitoring of UFF's network. The SCIFI network uses the eduroam as the authentication service.  The SCIFI controller coordinates data gathering from system logs, channel selection and access point's transmission power level services. SCIFI network allows an expressive reduction on a large scale wireless network deployment cost, which eases the deployment of bigger networks, with more APs. SCIFI network is used at UFF, Ouro Preto Federal University and Brazilian Navy, as well as in many different events. It have been proven to be a stable, low-cost and easy-to-install solution for controlling wireless APs. 

# UFF SCIFI Access Points Presented on the Datasets and Data Collection Dates 

We selected, for this study, all the APs located at one specific building from one of the UFF's campuses, called H building. Differently from the other buildings on campus that have professor's offices, laboratories, student unions and other university administration rooms, the H building has only classrooms. So, its occupation mainly occurs through lectures and exam applications. SCIFI network has 28 APs distributed over the 5 floors inside H building. Our data was obtained from the APs event logs. These logs were collected and stored at the SCIFI controller. Each AP sends a text file with all the management and control events information from their physical and data link layers. These data are requested and stored weekly by the controller. We collected data from 6 months, between April and September 2018.

# UFF SCIFI Acces Points Utilization Data Collectiona and Filtering and Dataset Construction

We collected all the event logs for the selected APs on the SCIFI controller. We filtered the text file to contain only information regarding the association, disassociation and deauthentication of mobile devices communicating with the access point since they mark the beginning and end of the data transmission between the AP e the mobile station. We observed that the disassociation message log did not always appear on the log data, although the deauthentication message always occurred in pair to the disassociation message. We also observed that whenever disassociation and deauthentication of mobile stations message appeared in the logs, both occurred in very close time intervals, with approximately 1 second difference between them. Therefore, we used deauthentication messages as the end of a connection mark between a mobile station and an AP, when there was no registered disassociation messages. Only a deep analysis would show the real reasons behind the absence of those disassociation messages in the logs, but we can point the user movement to an area with no network coverage as a possible cause.



# UFF SCIFI Acces Points Utilization Dataset Construction

After filtering and preprocessing event logs to contain only information related to the connection status between the mobile stations and the H's building APs, 
we create 2 datasets that compile information related to a daily occupancy history for APs during fixed time slots. We count the number of mobile stations associated to each AP during a 10 minutes time interval of a day. The number of mobile stations associated to an AP at a specific period of time x is the number of mobile devices that have been connected before time period x and have not disconnected, plus the number of mobile devices that have connected to the AP during the time period x. Considering 10 minutes interval, there are 144 time intervals in a day, resulting in 144 output features since we divided it by 10 minutes time intervals. Each time T_x represent a specific time interval of the day. Time T_0 represents the time slot between 00:00 and 00:10 and the rest follows it in a crescent order, always adding 10 minutes more when compared to the feature before its own time window. The exception is the feature $T_143, the last one, which as only nine minutes an then range from 23:50 to 23:59. 


Each instance of our datasets have 5 inputs and 144 output features. Month and day input features are numeric and show the date being presented in the instance. Feature  days of the week is categorical and indicates the day of the week of that instance (Monday to Sunday). Holiday input feature is boolean and indicates if the day is a normal semester day with lectures (value False) or a holiday (value True). AP Identification (Apid) input feature carries the access points identification and it informs to which specific H's building AP the occupancy history belongs to.

## Association Utilization Dataset

One Dataset is constructed containing the number of associated devices. The Association Utilization Dataset shows the number of wireless devices that were connected to a AP during a specific 10 minutes time slot. Each one of the 144 output features of a instance shows the number os wireless devices that were connected to a specific AP on the given date for the specific time slot. The wireless devices does not need to be connected during the whole time slot to be counted, it only need to stablish a connection ( generate a associantion log). Here is an example that shows a sample of the constructed datasets that shows the history of occupancy for different H building APs for different days and months.

![Image 2](https://github.com/midiacom/UFF-SCIFI-Datasets/blob/master/Utilization_Dataset_Example.PNG)

## Ocuppation Dataset

The second Dataset is constructed containing the APs occupation status. We can address the utilization problem as a classification problem whether an AP is occupied or not. Therefore, we apply a label binarization filter to our dataset, in order to transform each numeric label into a boolean output feature. To be classified as occupied (value 1), an AP needs to have at least one mobile station connected to it during the specified time slot. If no mobile station tries to connect to that AP during the whole duration of that day time slot, the AP is considered idle (value 0). Here is an example that shows a sample of the constructed datasets that shows the history of occupancy for different H building APs for different days and months.

![Image 3](https://github.com/midiacom/UFF-SCIFI-Datasets/blob/master/Occupation_Dataset_Example.PNG)

# Cite the Midiacom Lab UFF SCIFI Datasets

If you use ours Datasets in a scientific publication, we would appreciate citations to the following paper:


Bibtex entry:


# Special Thanks

We  acknowledge  and thank the  Rio  de  Janeiro  State  Science Foundation  (FAPERJ), Coordination for the Improvement of Higher Education Personnel (CAPES) and  the  Brazilian  National Science Council (CNPq) for financial support.
