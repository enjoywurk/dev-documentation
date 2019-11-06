# Cost Centers 

Cost centers in Wurk are represented as a tree. This tree can have any number 
of layers and any number of parent child releationships.  

You can find cost centers by loggin in as an admin and navigating to 
*Company Settings > Global Setup > Cost Centers*  

Then edit a cost center to view its tree:   
![Cost Center Tree](images/cost-center-tree.png)  

## APIs

#### List All
Retrieve a list of call centers by using the following API call: 
```bash
curl --request GET \
  --url 'https://secure.saashr.com/ta/rest/v2/companies/{companyId}/config/cost-centers?tree_index=0' \
  --header 'authentication: Bearer {bearer token} \
```
As documented here: https://secure.saashr.com/ta/docs/rest/public/#

This call returns the entire tree, relationships are represented by the `parent_id`. 
Within this structure every entity, including locations, in your business model is just another cost center. 

#### Create New Cost Centers 

Create a new cost center with the following API call: 
```bash
curl --request POST \
  --url 'https://secure.saashr.com/ta/rest/v2/companies/{companyId}/config/cost-centers/collection' \
  --header 'authentication: Bearer {bearer token} \
  --header 'content-type: application/json' \
  --data '{
	"cost_centers": [
		{
			"parent_cc": {
				"tree_index":0,
				"id": 4330039276
			},
			"name": "123 Street Drive",
			"time_allocation": true,
			"manning": 0.0,
			"gl_codes": [
				{
					"index": 0,
					"value": "2200"
				}
			],
			"visible": true,
			"custom_fields": [],
			"location_factor": 1.0,
			"contacts": [],
			"contact_address": {
				"country": "USA"
			},
			"use_employee_home_address": false,
			"state_assigned_tax_code": 0,
			"is_operating_and_reportable": false,
			"delivery_point_barcode": "00",
			"cost_center_skills": [],
			"job_settings": {
				"certified": false,
				"is_sub_contractor": false,
				"project_location": {
					"country": "USA"
				}
			}
		}
	]
}'
```

This API will not overwrite existing cost centers

#### Cost Center Jobs

In Wurk, there is an API for creating cost center jobs. However, we typically just use the cost centers to represent jobs.
So if our structure looks like this: 
```bash
Main Company
├── Location 1
├── Location 2
└── Location 3
    |── Manager
    └── Sales Associate
```

Both the manager and sales associate are still cost centers, but can be used to represent a job. 
We find this implementation to be more efficient and easy to understand

