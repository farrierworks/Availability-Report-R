# Availability Report

![GitHub repo size](https://img.shields.io/github/repo-size/farrierworks/Availability-Report-R)
![GitHub top language](https://img.shields.io/github/languages/top/farrierworks/Availability-Report-R)
![GitHub last commit](https://img.shields.io/github/last-commit/farrierworks/Availability-Report-R)

## Downloading data

1. Connect your USB drive to your DWAN computer.

2. In DRMIS Production, run the following transactions with the specified parameters:

    * **IE 36 - Display Vehicles**
        * _Class Type_: `002`
        * _Class_: `VEH_EQUIP`
        * _Vehicle Type_: `EV0309`, `EV0B54`, `EV0B68`, `EV0B80`, `EV0B82`, `EV0B94`, `EV0B97`, `EV0J06`, `EV0J07`, `EV0J08`, `EV0J31`, `EV0J35`, `EV0J36`, `EV0J37`, `EV0J38`, `EV0J44`, `EV0J46`, `EV0J81`, `EV0J82` and `EV0J83`
        * Once the transaction finishes running (may take several minutes), select all of the records, and click _Settings_, followed by _Show/Hide Classification_

    * **ZEIW29 - List Edit Display Notification (UDF)**
        * _Notification status_: `Outstanding`, `Postponed` and `In process`
        * _Planning plant_: `0001`
        * Once the transaction finishes running, add the _Equipment_ column
 
3. Export the results to Excel, and save the files to your USB drive as `ie36.csv` and `depot.csv`, respectively.

4. In DRMIS BEx Analyzer (DRMIS BW Production), run the following transactions with the specified parameters:
 
    * **[ZPM_0EQUIPMENT_7028_Q01] VOR Tactical - MPO Disposition**
        * _Force Element Hierarchy_: `[3663] Minister of National Defence` and `[REST_H] Not Assigned Force Element`
        * _Equip. Object Type_: `EV0309`, `EV0B54`, `EV0B68`, `EV0B80`, `EV0B82`, `EV0B94`, `EV0B97`, `EV0J06`, `EV0J07`, `EV0J08`, `EV0J31`, `EV0J35`, `EV0J36`, `EV0J37`, `EV0J38`, `EV0J44`, `EV0J46`, `EV0J81`, `EV0J82` and `EV0J83`
        * _Master Equip Index_: `X`
        * Once the transaction finishes running, right click on any table heading (e.g. _Equipment Number_), and click _Query Properties_:
            * In the _Navigational State_ tab:
                * In the _Columns_ field, right click on _Key Figures_ and click _Select Filter Value_. Move all but `Qty Held` from _Chosen Selections_ to _Displayed Key Figures_ (select each and click the left arrow icon)
                * Move `Plant` from _Free Characteristics_ to _Columns_ field
                * Right click on `Plant` and select properties. In the properties change `Display` from `Key` to `Text` and click _OK_
                * In the _Rows_ field, move all but `Equip. Object Type` to _Free Characteristics_ (select each and click the right arrow icon)
                * In the _Free Characteristics_ field, move `Equipment Number` and `User & Info Statuses` to _Rows_ (select each and click the left arrow icon)
                * Rearrange the _Rows_ field in the following order `Equipment Number`, `Equip. Object Type` and `User & Info Statuses`
            * The _Query Properties_ must look like the following:
            
            * ![alt text](https://github.com/Boniface316/Availability-Report-R/blob/plant_feature/img/query-prop.png?raw=true)

5. Select all of the table headings and rows, copy and paste into a new Excel file, and save it to your USB drive as `bex.csv`.

6. Disconnect your USB drive from your DWAN computer and connect it to your standalone computer (e.g. Dell XPS 13).

## Running the dashboard
7. Goto the folder where Availability-Report-R is located
8. Double click on `run.sh` and select `Run in Terminal`. Then right click on `http:\\###:##:##:##` and select `Open Hyperlink`
9. Upload the files and press `Create Report`

![alt text](https://github.com/Boniface316/Availability-Report-R/blob/plant_feature/img/runreport.gif?raw=true)
