# Getting Started

This wiki is the core documentation for integrating the Coaching and Student Temp APIs.

The API is built on the RESTful JSON framework.

All requests should use the HTTPS protocol.

Developers wishing to integrate with the platform will require API credentials.

_Please contact support to request an API developer account is setup._


***


# Authentication

Developers implementing this API will be issued with the following security credentials by Dashboard Technology:
* email
    * Your email address
* password
    * A strong password
* token
    * A unique hash token for your developer account

## Request
> **GET** api/v1/users/authenticate

`token`
> _string_    The developer token issued when creating your Developer account

`password`
> _string_    The password assigned to you

### Example Request
    http://api.dashboardtechnology.co.uk/api/v1/users/authenticate?password=Str0ngPa%24%24w0Rd&token=87y42bjweidhjbndmuggd

## Response
> **200** Response will be an object containing the secret_key. **Secret Keys are only valid for 7 days.**

    {"Response": $2a$10$ySdGj9aAcTwu9ia7sSWdHuFffnqbx5zGXXOtS43oVwuDm2D8M/C96}

> **401** Invalid security credentials supplied

    {"error":"Invalid credentials."}


***


# Get Organisations

You will need a valid secret key to access this method - See the [Authentication](#authentication)

## Request
> **GET** api/v1/organisations

`token`
> _string_    The developer token issued when creating your Developer account

`secret_key`
> _string_    The secret key issued via the Authentication request

### Example Request
    http://api.dashboardtechnology.co.uk/api/v1/organisations?token=87y42bjweidhjbndmuggd&secret_key=$2a$10$ySdGj9aAcTwu9ia7sSWdHuFffnqbx5zGXXOtS43oVwuDm2D8M/C96

## Response
> **200** Response will be a JSON object containing all organisations that the developer account has permission to access

`id`
> _integer_    The organisation ID

`name`
> _string_    The name of the organisation

    [{"id":12345,"name":"ACME LTD"},{...}]

> **401** Invalid security credentials supplied

    {"error":"Invalid credentials."}


***


# Get Payroll

To get the payroll for an organisation you will need a valid secret key and your developer account must have permission to access the data of the organisation requested.

You will need a valid secret key and your developer account must be configured correctly. See the [Authentication](#authentication)

## Request
> **GET** api/v1/payroll

`token`
> _string_    The developer token issued when creating your Developer account

`secret_key`
> _string_    The secret key issued via the Authentication request

`organisation_id`
> _integer_    The Organisation ID

`trans_date`
> _date_ (YYYY-MM-DD)    A specific transaction date _**optional**_

`sort`
> _string_    The ability to specify which field to sort the results by, default is 'id' _**optional**_

`fields`
> _string_    The ability to specify which fields to return, default is all fields are returned _**optional**_

`offset`
> _string_    The ability to paginate the resultset, default is offset=0 _**optional**_

`limit`
> _string_    The ability to paginate the resultset, default is limit=20 _**optional**_

### Example Request
    http://api.dashboardtechnology.co.uk/api/v1/payroll?token=87y42bjweidhjbndmuggd&secret_key=$2a$10$ySdGj9aAcTwu9ia7sSWdHuFffnqbx5zGXXOtS43oVwuDm2D8M/C96&organisation_id=12345&trans_date=2017-01-01&sort=surname,+forenames&fields=pay_group,employee_no&offset=0&limit=20

## Response
> **200** Response will be a JSON object containing all payroll results for the supplied organisation and parameters

**The total number of results are sent back in the response via the custom HTTP header: X-Total-Count.**

`id`
> _integer_   Payroll ID

`pay_group`
> _string_    Pay Group

`employee_no`
> _integer_    Employee Number

`forenames`
> _string_    Employee Forenames

`surname`
> _string_    Employee Surname

`trans_date`
> _date_ (YYYY-MM-DD)    Payroll Transaction Date

`pay_code`
> _string_    Pay Code

`hours_value`
> _float_    Hours/Value

`activity_code`
> _string_    Activity Code

`status`
> _string_    Payroll Status

`acc_code`
> _string_    Account Code

`appt`
> _string_    Appointment

`rate`
> _float_    Rate of Pay

`payslip_value`
> _float_    Payslip Value

`pay_code_desc`
> _string_    Pay Code Description

`date_worked`
> _date_ (YYYY-MM-DD)    Date Worked

`start_time`
> _time_    Start Time

`end_time`
> _time_    End Time

`contract_start_date`
> _date_ (YYYY-MM-DD)    Contract Start Date

### Example Response
    [
        {
             "id":123,
             "pay_group":"A",
             "employee_no":"23456",
             "forenames":"Bob",
             "surname":"Smith",
             "trans_date":"2016-09-01",
             "pay_code":"WL33",
             "hours_value":"30.00",
             "activity_code":"BL1",
             "status":"AT",
             "acc_code":"UK35",
             "appt":"",
             "rate":"125.95",
             "payslip_value":"1245.32",
             "pay_code_desc":"Administration Services",
             "date_worked":"2016-09-30",
             "start_time":"10:00:00",
             "end_time":"18:00:00",
             "contract_start_date:"2015-01-01"
        },
        {...}
    ]

> **401** Invalid security credentials supplied

    {"error":"Invalid credentials."}

***

# HTTP Status Codes
* 200 – OK – Everything is working
* 201 – OK – New resource has been created
* 204 – OK – The resource was successfully deleted

* 304 – Not Modified – The client can use cached data

* 400 – Bad Request – The request was invalid or cannot be served
* 401 – Unauthorized – The request requires an user authentication
* 403 – Forbidden – The server understood the request, but is refusing it or the access is not allowed
* 404 – Not found – There is no resource behind the URI.
* 422 – Unprocessable Entity

* 500 – Internal Server Error
