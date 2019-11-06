# Employee Management

Fields ignored during employee creation: 'Id', 'Status', 'Terminated', 'Links'
Fields ignored during employee updates: 'id', 'status', 'terminated', 'links', 'EIN', 'external_id'
Note that employees can not be terminated via the API. 

### Add and Remove Employees From Jobs

Because we are using cost centers as jobs you can add or remove an employee from a job by 
calling PUT /employees/{id} and updating the `cost_centers_info` object. 

```bash
curl --request PUT \
  --url https://secure.saashr.com/ta/rest/v2/companies/%7CCalebTest/employees/4333104198 \
  --header 'authentication: Bearer {bearer token}' \
  --header 'content-type: application/json' \
  --data '{
  "id": 4333104198,
  "employee_id": "119",
  "username": "JSchuch12",
  "first_name": "John",
  "last_name": "Schuch",
  "primary_account_id": 4333104198,
  "status": "Active",
  "locked": false,
  "force_change_password": true,
  "primary_email": "msajn@enjoywurk.com",
  "social_security": "540-23-8612",
  "first_screen": {
    "id": "SCREEN:101"
  },
  "address": {
    "address_line_1": "900 Colorado",
    "country": "USA",
    "city": "Denver",
    "state": "CO",
    "zip": "80205"
  },
  "use_separate_mailing_address": false,
  "timezone": "America/Denver",
  "dates": {
    "hired": "2017-01-01",
    "started": "2017-01-01",
    "birthday": "1990-01-01"
  },
  "managers": [
    {
      "index": 0,
      "empl_ref": {
        "account_id": 4333098987
      }
    },
    {
      "index": 1,
      "empl_ref": {
        "account_id": 4333098987
      }
    }
  ],
  "cost_centers_info": {
    "defaults": [
      {
        "index": 1,
        "value": {
          "id": 4330039290
        }
      }
    ]
  },
  "ein": {
    "id": 34500226
  },
  "add_to_new_hire_export": true,
  "managed_cost_centers_enabled": false,
  "national_id_numbers": [
    {
      "type": "SSN",
      "value": "540-23-8612",
      "primary": true
    }
  ]
}'
```

### Update Employee Compensation

Retrieve all base compensations using this API call: 
```bash
curl --request GET \
  --url https://secure.saashr.com/ta/rest/v2/companies/%7CCalebTest/compensation/history \
  --header 'authentication: Bearer {bearer token}' \
  --header 'content-type: application/json' \
```

You can update an employees base compensation with the following API call: 
```bash 
curl --request PUT \
  --url https://secure.saashr.com/ta/rest/v2/companies/%7CCalebTest/compensation/history/201810094333098986 \
  --header 'authentication: Bearer {bearer token}' \
  --header 'content-type: application/json' \
  --data '{
      "id": 201810094333098986,
      "employee": {
        "account_id": 4333098986
      },
      "effective_from": "2018-10-09",
      "amount": 15.0,
      "hourly_pay": 15.0,
      "amount_period": "HOUR",
      "time": 7488000000,
      "time_period": "YEAR",
      "_links": {
        "self": "https://secure2.saashr.com/ta/rest/v2/companies/33593369/compensation/history/201810094333098986"
      },
      "currency": "USD"
}'
```