5. List of accounts
- information to be marked
- [x] Customer name (user_name) : Must be seen as a physical name by referring to the customer ID.
- ~~If you press the customer name, go to the user details screen.~~
- [x] Broker_name : Example) It should be seen as a real name by referring to OO securities, 'brokers.json'.
- [x] Account number: Except for the two characters before and after, masking is required with '*' characters according to the number of characters.
- [x] Account status: Example) In operation, it should be shown by its actual name by referring to 'accountStatus.json'.
- [x] Account name (name): Account name.
- [x] Assets: Example) 123,123,123
- [x] Payment amount: Example) 123,123,123
- [x] Account activation status (is_active): Account activation status
- [x] Account opening date (created_at):
- Features to be implemented
- [x] The list should be able to filter the broker name, account activation status, and account status.
- The [ ] list page must be searchable.(You can search it, but...) How can I convert kr to raw data?)
- Implemented using the full-text search API of 'json-server'.
- - 예시 : GET [http://localhost:3000/accounts?q=South](http://localhost:3000/accounts?q=South)
- [x] It should be a pageation.
- Implemented using 'json-server''s Paginate API.
- - 예시 : GET [http://localhost:3000/accounts?\_page=2&\_limit=20](http://localhost:3000/accounts?%5C%5C_page=2&%5C%5C_limit=20)
6. Details
- [x] You can display most of the available information on the details page of each user's account.
7. Conditions
- [x] The Side menu should highlight the menu that corresponds to the screen you are currently viewing.
- [x] Even if you reload, you must remain logged in, and depending on your status, the screen you have been staying in should be visible.
- [x] Pressing the account number in the account list takes you to the account details screen.
- ~~Click the user name in the account list to go to the user details.~~
- ~~The user's account list must be visible in the user details.~~
- You must be able to filter by each account status in the account list.
- [x] The total asset amount of an account with a positive return should be shown in red, black if it is equal to the principal, and blue if it is negative.
- [x] The actual broker name (OO Investment & Securities) corresponding to broker_id should be visible in the account list.
8. Additional Implementations
- [x] The account number corresponding to the format of 'brokerFormat.json' is indicated (e.g. 123-123-123123-10).
- Handling Contextual Exceptions

Requirements

- Must be ~~React.js based.~~
- ~Node.js LTS environment~
- ~~Recommend using UI libraries or frameworks such as [antd] (https://ant.design/) or [tailwindcs] (https://tailwindcss.com/))~~
- ~~Follow the basic design system of your library, but expand it and develop it if necessary.~~
- ~~A separate API server development is not required.~~
- Development using json-server that comes with the assignment~
- ~~~ API response values are always assumed to be a normal response, but~~ There are additional points due to exception handling such as server error response, failure response, timeout, etc.
- ~~It should work fine on a typical user PC (1280x1024 or later) screen.~~
- ~~If you need any conditions, you can add them.~~
- ~~There are no conditions for use such as specific packages.~~
- ~~By default, you can use a newer version than the package version in your given environment.~~
- Only authorized users must be able to create, query, modify, delete (CRUD).
- ~~A separate membership function is not required.~~
- ~~Development after creating a random user by referring to the API call example~~
