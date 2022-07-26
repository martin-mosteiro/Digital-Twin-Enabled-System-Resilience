[![DT_fast_icon](https://user-images.githubusercontent.com/18548065/180711420-8e03247e-5803-4943-8a48-6b4e856b974f.png)](https://player.vimeo.com/video/733100345)

## Project duration

1 March 2021 - 30 September 2024

## Stakeholders
This project is carried out as part of [Future Resilient Systems Module 1.4 "Digital Twin-Enabled System Resilience"](https://frs.ethz.ch/research/cyber-physical-systems/digital-twin-enabled-system-resilience.html).

### Execution
* National University of Singapore (NUS)
* Future Resilient Systems (FRS)

### Funding & programme coordinators
* National Research Foundation Singapore (NRF)

### Collaborators
* Singapore-ETH Centre

## Objective
With the increasing frequency and magnitude of major disruptive events in urban areas, the resilience of the built environment against climate change impacts and associated disruptions has received increasing attention in recent years [1]. As a low-lying, tropical island with a hot and humid climate, Singapore is particularly vulnerable to the impact of climate change [2]. In order to mitigate the effects of climate change on building occupants' health and well-being, resilient cooling is of principal importance to maintain indoor environmental quality against unexpected events such as extreme weather conditions, heat waves, and power outages [3]. Such vulnerabilities have been compounded by the COVID-19 pandemic and the societal shifts it has caused, leading to changes in the way energy is used and therefore putting further stress on existing energy infrastructure.

As a demonstrator for a digital-twin enabled approach to district energy resilience, a digital twin of a university campus in Singapore is under development. The campus comprises around 300 buildings including a variety of building use types such as classrooms, laboratories, offices and residential buildings as well as a variety of amenities. The area is currently served by a number of district cooling networks of different scales. The digital twin will form the basis for a new approach to evaluate the vulnerability, efficiency, and resilience of future urban districts in the tropics.

A digital twin is a virtual representation of a physical system (and its associated environment and processes) that is updated through the exchange of information between the physical and virtual systems [4]. Originating in the aerospace field, the digital twin concept has found applications in a number of different sectors, including health, meteorology, manufacturing and process technology, education, cities, transportation, and energy [5]. A number of works in the literature have focused on the development of digital twins to aid urban planning and citizen engagement [6, 7, 8, 9]. Digital twins have also found applications in district energy systems, particularly in system planning [10], energy management and optimization [11], and model predictive control [12, 13].

The present project seeks to study how both buildings and energy systems can help build resilience through coupling advanced numerical models and real-time data. As a first step in the development of this framework for district energy resilience, this paper focuses on the digital twin of the built environment. Previous work shows heat waves, power outages, and pandemics are some of the main types of disruptions affecting the built environment [3]. In order to demonstrate the possibilities of the approach presented, the long-term effects of climate change and the shift to increasingly working from home after the COVID-19 pandemic on the energy demands of a district were selected as test cases for this project. The platform is therefore intended to allow planners and system operators to not only analyze the district’s past and present energy performance, but also interact with the systems and explore the effect of different disruption scenarios through simulations.

## Team
### Principal Investigators
* Prof. Rudi Stouffs (PI, NUS Department of Architecture)
* Prof. Clayton Miller (co-PI, NUS Department of the Built Environment)

### Research fellows
* Dr. Martín Mosteiro-Romero (NUS, FRS)
* Pradeep Alva (NUS, FRS)

### Research fellows
* Prof. Adrian Chong (NUS)
* Prof. Filip Biljecki (NUS)

## Project structure and output
The digital twin comprises a user interface for real-time data visualization along with physical models of the buildings in the district, their occupants, and the energy demands that arise as a result of their activities. The project is therefore divided into four sections, each focusing on one aspect relevant to the digital twin's development.

### Building 3D model
<img src="https://user-images.githubusercontent.com/18548065/180714022-f525e330-ef4b-46b4-9797-e699c10dd6fd.png" width="650" />

The process starts with extracting 2D input shapefiles from OpenStreetMap (OSM). This process generally takes many iterations to check the validation of the data. It is possible that the OSM attributes do not correlate to physical reality. Hence, building typology and the number of floors were specifically checked and updated as required. The geometry from these shapefiles is two-dimensional (level of detail = 0), basically simple polygons of building footprints. Thus, the polygons were imported to FME with a default shapefile reader and extruded to their building heights. Later, a writer was used to convert the 3D geometry into CityGML and Cesium 3D Tile format. Detailed IFC-BIM models (LOD3) of a few buildings on campus were combined with the rest of the model (LOD1) using an IFC to CityGML work pipeline).

All the converted 3D tiles were used to create the web map application as the digital twin dashboard. In addition, time-based sensor data stored in the InfluxDB cloud (an open-source cloud-native serverless platform) was accessed through a robust API to display high-frequency building information. This real-time sensor data was acquired from weather stations installed in campus. These capture indoor temperature, humidity etc. at a 10-minute frequency. Finally, Highcharts (a multiplatform charting JavaScript library) was used to display the simulation results and live data interactively on the dashboard (Chaturvedi & Kolbe, 2019; Würstle et al., 2020).

#### Publications
* Alva P., Mosteiro-Romero M., Miller C., and Stouffs R., 2022. “Digital twin-based resilience evaluation of district-scale archetypes: A COVID-19 scenario case study using a university campus pilot”. In: _POST-CARBON, Proceedings of the 27th CAADRIA Conference_, Sydney, Australia, April 9-15 2022, vol 1, pp. 525-534.

### Energy demand model
<img src="https://user-images.githubusercontent.com/18548065/180712380-8a4a074f-7a28-4bba-9de5-c28d956768bb.png" width="400" />

In order to project future demands in the case study district under different scenarios, a building energy demand model of the case study area was developed using the open-source tool [City Energy Analyst (CEA)](cityenergyanalyst.com). This tool was selected due to its lightweight energy demand model and simplified inputs. This software has previously been used to assess the effects of local climate and changes in occupancy patterns on energy demand, both desirable characteristics in this project.

Since detailed information about the building envelope and system operation were not available, these parameters were assigned using brute force optimization with discrete input parameters obtained from the CEA archetypes database. The parameters to be calibrated were selected from a previous sensitivity analysis of the tool's thermal models. Each combination of parameters was assessed by the coefficient of variation of root-mean square error (CV(RMSE)) using hourly measurements of electricity and cooling demand. The calibrated model was found to perform adequately for the majority of the buildings, with the expectation of improved model performance as further data are collected.

#### Publications
* Mosteiro-Romero, M., Alva, P., Miller, C. and Stouffs, R., 2022. “Towards occupant-driven district energy system operation: A digital twin platform for energy resilience and occupant well-being." In: _PLEA 2022: Will Cities Survive?_, Santiago, Chile, November 23–25 2020.
* Mosteiro-Romero M., Miller C., Chong A., and Stouffs R., 2022. "Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization". Submitted to _Applied Energy_.

### Building occupant modeling
<img src="https://user-images.githubusercontent.com/18548065/180719435-f171fdcd-4ff7-48d8-ac58-cedad4683965.png" width="650" />

Occupant presence was first estimated using WiFi connection counts from each building in the case study. k-means clustering was used to assign typical WiFi connection profiles to each day of the year, generating a yearly profile of occupancy that differentiated between weekdays, weekends, and public holidays, as well as between semesters and holiday periods.

The measured electricity loads were then used to fit a regression model to estimate electricity demand as a function of time of day and building occupancy. These occupant profiles and electricity demand schedules are then inputted back into the building energy demand model for the thermal load calculation.

In order to analyze the relationship between occupants' thermal comfort and activity location choices, an agent-based model of building occupants as campus scale is being developed. The collected WiFi data is being used to extract activity patterns of the users of the campus. These are being coupled with data from field studies in NUS on occupants' feedback on their thermal preferences collected through the [Cozie app](https://cozie.app/). These data are being used to analyze occupants' thermal comfort behavior decisions on campus. The campus-scale agent-based model will allow us to explore occupant comfort in the building stock and let occupants' thermal comfort be the driver of the types of choices in activity location that we have so far determined using a top-down approach.

#### Publications
* Mosteiro-Romero M., Miller C., Chong A., and Stouffs R., 2022. "Elastic buildings: Calibrated district-scale simulation of occupant-flexible campus operation for hybrid work optimization". Submitted to _Applied Energy_.

### Digital twin dashboard and data visualization
<img src="https://user-images.githubusercontent.com/18548065/180699210-ad956bba-2c69-4f9d-8177-3444abed5e1f.JPG" width="650" />

We are developing a digital twin platform for decision making through a web application for NUS campus with around 300 buildings. The platform provides 3D visualisations of the buildings and energy infrastructure on campus, real-time data from sensors, energy demand simulation results, occupancy rates, and scenario visualizations.

The digital twin dashboard is set up using XAMPP (an open-source cross-platform web server solution stack package) for testing. The campus model in 3D Tile format and the metadata acquired from energy demand simulations are used for styling in JavaScript. Further visualisation is customised within JavaScript as specified in Cesium 3D Tile format.

The dashboard display can switch between scenes thematically based on building typology, cooling loads, highlighting individual building typology (academic, residential, office etc.), thermal network of building cluster, energy-use intensity, and its ratio to occupancy. Tables 1-2 show the attributes assigned to each building in the campus - Unique building ID, gross floor area, occupancy, building height, number of floors, base simulation results (building electricity consumption, cooling load), WFH and OFA based cooling load results.

#### Publications
* Alva P., Mosteiro-Romero M., Miller C., and Stouffs R., 2022. “Digital twin-based resilience evaluation of district-scale archetypes: A COVID-19 scenario case study using a university campus pilot”. In: _POST-CARBON, Proceedings of the 27th CAADRIA Conference_, Sydney, Australia, April 9-15 2022, vol 1, pp. 525-534.

## Other publications
* Alva P., Biljecki F., and Stouffs R., 2022. "Use cases for district-scale digital twins”. Full paper submitted to SDSC & 3DGeoinfo conference 2022.

## Acknowledgments
The research was conducted at the Singapore-ETH Centre, which was established collaboratively between ETH Zürich and the National Research Foundation Singapore. This research is supported by the National Research Foundation, Prime Minister's Office, Singapore under its Campus for Research Excellence and Technological Enterprise (CREATE) program.
