Authentication
===
	-Developers implementing this API will be issued with the following security credentials by Dashboard Technology:

## Parameters
	-username
		Developer username
	-password
		Developer password

## Method
	- GET api/v1/authenticate

## Example Request
  	/api/v1/users/authenticate?username=developer&password=Str0ngPa%24%24w0Rd

	## Response

	-200 Response will be an object containing the token. Tokens are only valid for 7 days.
	{"token": $2a$10$ySdGj9aAcTwu9ia7sSWdHuFffnqbx5zGXXOtS43oVwuDm2D8M/C96}

	-401 Invalid security credentials supplied
	{"error":"Invalid credentials."}

Clients Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
    -id
        Client specific id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name

## Method
	- GET api/v1/clients

## Example Request
  	api/v1/clients?token=sjahsjhdjashdjasdg7677&page=1&limit=20&sort=id

	## Response

	-200 Response will be an client object.
	[
	  {
		"id": 13,
		"name": "Brentford FC CST"
	  }
	]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	 -401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

Locations Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
    -id
        Location specific id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/locations

## Example Request
  	api/v1/locations?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&page=1&limit=2&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an location object.
	[
      {
        "id": 247,
        "name": "Demo Location",
        "address1": "39 - 51 Highgate Road",
        "address2": "",
        "address3": "London",
        "postcode": "NW5 1RT",
        "created_at": "2012-02-19T15:02:20.813Z",
        "updated_at": "2016-02-19T12:10:38.989Z",
        "full_name": "Jo Bloggs",
        "contact_number": "02076654432"
      },
      {
        "id": 247,
        "name": "Demo Location",
        "address1": "39 - 51 Highgate Road",
        "address2": "",
        "address3": "London",
        "postcode": "NW5 1RT",
        "created_at": "2012-02-19T15:02:20.813Z",
        "updated_at": "2016-02-19T12:10:38.989Z",
        "full_name": "Henry Peters",
        "contact_number": "07793111622"
      }
	]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"

Bookings Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
    -id
        Booking specific id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/bookings

## Example Request
  	api/v1/bookings?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&page=1&limit=2&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an client object.
	[
      {
        "id": 34822,
        "booking_id": null,
        "student_id": 778,
        "booking_type": null,
        "cancellationCode": null,
        "hoursBooked": null,
        "date_booked": null,
        "created_at": "2012-02-19T15:11:47.596Z",
        "updated_at": "2012-02-19T15:13:21.003Z",
        "startDate": "2012-02-19",
        "starttime": "16:00:00",
        "student_firstname": "Coach1",
        "student_surname": "DemoDT",
        "reason_description": null
      },
      {
        "id": 34823,
        "booking_id": null,
        "student_id": 778,
        "booking_type": null,
        "cancellationCode": null,
        "hoursBooked": null,
        "date_booked": null,
        "created_at": "2012-02-19T15:12:02.173Z",
        "updated_at": "2012-02-19T15:13:28.579Z",
        "startDate": "2012-02-19",
        "starttime": "17:00:00",
        "student_firstname": "Coach1",
        "student_surname": "DemoDT",
        "reason_description": null
      }
    ]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"

Students Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
    -id
        Student specific id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/students

## Example Request
  	api/v1/students?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&page=1&limit=2&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an client object.
	[
      {
        "id": 773,
        "user_id": 901,
        "surname": "User",
        "firstname": "Admin",
        "mobileNo": null,
        "DOB": null,
        "sex": null,
        "created_at": "2012-02-19T14:29:53.689Z",
        "updated_at": "2012-02-19T14:29:53.689Z",
        "ethnicity_id": null,
        "disability": false,
        "ethnicity_value": null,
        "address1": null,
        "address2": null,
        "address3": null,
        "postcode": null,
        "email": "adminb@dashboardtechnology.co.uk"
      },
      {
        "id": 774,
        "user_id": 902,
        "surname": "User",
        "firstname": "Admin",
        "mobileNo": null,
        "DOB": null,
        "sex": null,
        "created_at": "2012-02-19T14:39:32.406Z",
        "updated_at": "2012-02-19T14:39:32.406Z",
        "ethnicity_id": null,
        "disability": false,
        "ethnicity_value": null,
        "address1": null,
        "address2": null,
        "address3": null,
        "postcode": null,
        "email": "pskelhorn@brentfordfccst.com_rm"
      }
	]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"

Timesheets Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
    -id
        Timesheet specific id(optional)
	-bookingID
		the booking that the timesheets relate to(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/timesheets

## Example Request
  	api/v1/timesheets?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&bookingID=2516&page=1&limit=1&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an client object.
	[
      {
        "id": 345,
        "booking_id": 2516,
        "contactName": "Mr Brandreth (SCH)-01895671990",
        "bookingType": "Curriculum Coaching",
        "which_employer_approved": null,
        "comment": null,
        "pay_grade_title_id": null
      }
    ]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"
	 
Agency Project Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
        
	-id
		the agency project id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/agency_projects

## Example Request
  	api/v1/agency_projects?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&id=2516&page=1&limit=1&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an agency project object.
	[
    {
        "id": 1,
        "name": "New agency",
        "description": "description",
        "status": "A",
        "position": 1,
        "created_at": "2018-05-03T10:51:10.966Z",
        "updated_at": "2018-05-03T10:51:10.966Z"
    }
]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"
	 
Session Group Endpoint
===

## Parameters
	-token
		Developer token that are valid for 7 days
	-clientID
        the football club the data is requested for, the developer must have access to the client
        
	-id
		the session group id(optional)
	-page
	    default: 0
		  Ex. page=20
		  - The page number of results to return based on limit
	- limit
	    default: 20
		- Limit the number of rows/response
		  Ex. limit=25
	-sort
	    default: id, others available fields(:name)
		- sorting the rows/response specify on sort value
		  Ex. sort=name
    -created_at
	    default: nil
		- querying to locations table by date range(:created_at)
		  Ex. created_at>='2012-02-01', created_at<='2012-02-31'
    -updated_at
	    default: nil
		- querying to locations table by date range(:updated_at)
		  Ex. updated_at>='2012-02-01', updated_at<='2012-02-31'

## Method
	- GET api/v1/agency_projects

## Example Request
  	api/v1/agency_projects?token=5961f27f9540498bfd445f895fc017d490cd3bd8ec54a2fc&clientID=13&id=2516&page=1&limit=1&sort=id&created_at>='2012-02-01'

	## Body Response
	-200 Response will be an session group object.
	[
    {
        "id": 1,
        "name": "session group",
        "description": "description",
        "status": "A",
        "position": 1,
        "created_at": "2018-05-03T10:51:29.613Z",
        "updated_at": "2018-05-03T10:51:29.613Z"
    }
]

	## Header Response
		x-page → 2 (the current page number)
		x-per-page → 20 (total records per page)
		x-total → 325 (total number of records)

	-401 Invalid token supplied
	 "error": "Invalid token, please re-authenticate to generate a new token"

	-401 Token expired
	 "error": "Expired token, please re-authenticate to generate a new token"

	-401 Developer doesn't have access to clients
	 "error": "API account doesn't have access to any clients"



