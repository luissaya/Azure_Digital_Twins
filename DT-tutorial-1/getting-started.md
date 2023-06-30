# Tutorial 1: Getting started with DT
[Reference](https://learn.microsoft.com/en-us/azure/digital-twins/quickstart-azure-digital-twins-explorer)

## Prerequisites
- Azure subscription, create one from [here](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Download the resources:
  - [Building.json](./resources/Building.json): This is a model file that digitally defines a building. It specifies that buildings can contain floors.
  - [Floor.json](./resources/Floor.json): This is a model file that digitally defines a floor. It specifies that floors can contain rooms.
  - [Room.json](./resources/Room.json): This is a model file that digitally defines a room. It has a temperature property.
  - [buildingScenario.xlsx](./resources/buildingScenario.xlsx): This spreadsheet contains the data for a sample twin graph, including five digital twins representing a specific building with floors and rooms.

## Set up Azure Digital Twins

### Create an Azure Digital Twins instance
Create a new instance of Azure Digital Twins using the [Azure portal](https://portal.azure.com/).
1. Create a resource in the Azure services home page menu.
2. Search for azure digital twins in the search box, and choose the Azure Digital Twins service
3. Fill in the fields on the Basics tab of setup, including your *Subscription*, *Resource group*(a Resource name for your new instance) and *Region*. Check the Assign Azure Digital Twins Data Owner Role box to give yourself permissions to manage data in the instance.
4. Select Review + Create to finish creating your instance.
5. Check the summary page showing the details. Confirm and create the instance by selecting Create.
### Open instance in Azure Digital Twins Explorer
- Use the Go to resource button to navigate to the instance's Overview page in the portal.
- Next, select the Open Azure Digital Twins Explorer (preview) button.
- This will open Azure Digital Twins Explorer in a new tab.
- Azure Digital Twins Explorer might automatically connect to your instance. If not, you'll see the following screen asking you to specify an Azure Digital Twins URL, enter https:// into the field, followed by the host name of your instance (this can be found back on the instance's Overview page in the portal).

## Build out the sample scenario
### Models
Models are generic definitions for each type of entity that exists in your environment. It's needed one model definition describing what a Building is, one model definition describing what a Floor is, and one model definition describing what a Room is.

Models for Azure Digital Twins are written in Digital Twin Definition Language (DTDL), a data object language similar to JSON-LD. Each model describes a single type of entity in terms of its properties, telemetry, relationships, and components.  
  
**Upload the models (.json files)**
  - In the Models panel, select the Upload a Model icon that shows an arrow pointing upwards.
  - In the Open window that appears, navigate to the folder containing the downloaded .json files on your machine.
  - Select Building.json, Floor.json, and Room.json, and select Open to upload them all at once.
  You can select View Model from any of the models' options to see the DTDL code that defines each model type.
### Twins and the twin graph
The previous definitions can be used to create digital twins for the elements in your environment.
**Import the graph (.xlsx file)**
  - In the Twin Graph panel, select the Import Graph icon that shows an arrow pointing into a cloud.
  - In the Open window, navigate to the buildingScenario.xlsx file you downloaded earlier. This file contains twin and relationship data for the sample graph. Select Open. After a few seconds, Azure Digital Twins Explorer opens an Import view that shows a preview of the graph to be loaded.
  - To finish importing the graph, select the Save icon in the upper-right corner of the graph preview panel.
  - Make sure you see the following dialog box indicating that the import was successful before moving on.
  - To see the graph, select the Run Query(select * from digitaltwins) button in the Query Explorer panel, near the top of the Azure Digital Twins Explorer window.
The circles (graph "nodes") represent digital twins. The lines represent relationships.  
  
**Add another twin**
Start by selecting the model that defines the type of twin you want to create. In the Models panel on the left, open the options menu for the Room model. 
- Select Create a Twin to create a new instance of this model type.
- Enter Room2 for the New Twin name and select Save. 
- Add a relationship to show that Floor1 contains Room2.
- Use the CTRL/CMD or SHIFT keys to simultaneously select Floor1 and Room2 in the graph. When both twins are selected, right-click Room2 and choose Add relationships.
- This will open a Create Relationship dialog that's pre-filled with the details of a "contains" relationship from Floor1 to Room2. Select Save.  
  
**View twin properties**
You can select a twin to see a list of its properties and their values in the Twin Properties panel.
- Room0 has a temperature of 70.
- Room1 has a temperature of 80.
- Room2 doesn't have values set for its properties yet, since this twin was created manually. To set its property values, edit the fields so that humidity is 50 and temperature is 72. Select the Save icon.

### Query changing IoT data
can query your twin graph to answer questions about your environment, using the SQL-style Azure Digital Twins query language.  
Start by running a query to see how many twins in your environment have a temperature above 75.
```SQL
SELECT * FROM DIGITALTWINS T WHERE T.Temperature > 75
```
only Room1 shows up in the results here.

**Edit temperature data**
First, rerun the following query to select all digital twins. This will display the full graph again in the Twin Graph panel.
```SQL
SELECT * FROM DIGITALTWINS
```
Select Room0 to bring up its property list in the Twin Properties panel. Change the temperature value from 70 to 76, and select the Save icon to update the temperature.


**Query to see the new result**
```SQL
SELECT * FROM DIGITALTWINS T WHERE T.Temperature > 75
```
Both Room0 and Room1 should show up in the result.

## Clean up resources
If you don't need your Azure Digital Twins instance anymore, you can delete it using the Azure portal.
Navigate back to the instance's Overview page in the portal. (If you've already closed that tab, you can find the instance again by searching for its name in the Azure portal search bar and selecting it from the search results.)
Select Delete to delete the instance, including all of its models and twins.