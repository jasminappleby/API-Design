# API Design Task

## Description and Considerations

Letting me move ltd. is a letting agency helping people with their moving needs.
The API has been created to facilitate the navigation and data management for the users of Letting me move ltd., employees and clients alike.
It is based on a relational database, thus the one implemented is using SQL.

## Schema

For our Schema Tables, we took a UNF to 3NF approach to create them. This enabled us to split up the data attributes within the database more logically. 

> Key: The top line is the header of the Schema Table. This will also be in bold. 
> PK = Primary Key
> FK = Foreign Key

### UNF 				
				
|**person**|**address**|**street address**|
|-------|--------|----------|
|age  |owner| postcode |
|name|
|num_of_ppl|		


1NF		
		
|**person**	|**address**|
|---------------|--------|
|f_name	  	|house_number|
|l_name	  	|street|
|age	     	|city|
|num_of_ppl	|county|
|resident 	|country|
|	        |postcode|


2NF
|	|**person**|
|---------------|--------|
|pk	|persID|
|	|f_name|
|	|l_name|
|	|age|
|	|num_of_ppl|
|fk	|resID|


|	|**resident**|
|---------------|--------|
|pk	|resID|
|	|owner|
|	|tenant|


|	|**address**|
|---------------|--------|
|pk	|addressID|
|	|house_number|
|	|street|
|fk	|cityID|
|fk	|countyID|
|fk	|countryID|
|	|postcode|


|	|**city**|
|---------------|--------|
|pk	|cityID|
|	|city|



|	|**county**|
|---------------|--------|
|pk	|countyID|
|	|county|



|	|**county**|
|---------------|--------|
|pk	|countryID|
|	|country|


3NF	
		
|	|**person**|**type**|
|---------------|--------|-------|
|pk	|persID	|int|
|	|f_name	|varchar(50)|
|	|l_name	|varchar(50)|
|fk	|ageID	|int|
|	|num_of_ppl	|int|
|fk	|resID	|int|


|	|**age**|**type**|**age groups**|
|-----|-----|-----|------|
|pk	|ageID	|int	
|	|youth	|int	|18-24|
|	|young_adult	|int	|25-34|	
|	|adult	|int	|35-59|
|	|senior	|int	|60+|


|	|**resident**| **type**|	
|-----|-----|-----|
|pk	|resID	|int|
|	|owner	|boolean|
|	|tenant	|boolean|


|	|**house**|**type**|
|-----|-----|-----|
|pk	|houseID	|int|
|fk	|addressID|int|
|fk	|resID	|int|
|    |size	|int|



|	|**address**|**type**|	
|-----|-----|-----|
|pk	|addressID	|int|
|	|house_number	|varchar(50)|
|	|address_line_1	|varchar(150)|
|	|address_line_2	|varchar(150)|
|fk	|cityID	|int|
|fk	|countyID	|int|
|fk	|countryID	|int|
|	|postcode	|varchar(8)|
|fk	|houseID	|int|


|	|**neighbourhood**|**type**|
|-----|-----|-----|
|pk	|neighbourhoodID	|int|
|fk	|addressID	|int|


## API Requests 

--- Store people, houses and addresses

|**Path**        |**HTTP verb**   |**Action**     |**Description**|
|-----|------|-------|------|
|/owner      |post        |create      |adds new owner to database|
|/tenant     |post        |create      |adds new tenant to database|


--- Look up a house, it’s address and owner

|**Path**        |**HTTP verb**   |**Action**     |**Description**|
|-----|------|-------|------|
|/owner/:id  |get     |show        |shows info about a certain owner|
|/tenant/:id |get     |show        |shows info about a certain tenant|
|/house/:id  |get     |show        |shows info about a certain house|


--- Look up people in our neighbourhood within certain age brackets and with specific household sizes
Path                
/letmemoveltd/accounts/searchType=young_adult&neighbourhood=POSTCODE%5E1591996=1&radius=0.5&householdSize=2
    
HTTP verb   
get     
Action      
index       
Description
displays a list of all people within a certain neighbourhood within certain age brackets and with specific household sizes

## HTTP Verbs and Paths


