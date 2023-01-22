# Customer Managemen
# How to set up and run your environment
## Client Preferences

**Recommended running on NodeJS 16.14.2.**

### Installing and running

## Server Preferences

## Installing and running

**npm run will initialize db information when initialized, so make sure to perform [http://localhost:4000/users/signup](http://localhost:4000/users/signup) with the same application as Postman to log in. If you don't do npm run, you can log in using the ID and password below.**

You must install and run the server and client, respectively.

1. How to install and run the server

```
// In the root folder
cd server && npm ci
npm start

```

1. How to install and run the client

```
// In the root folder
cd preface && npm ci
npm run dev

```

1. Login information

```
{
"email": "newface@dco.com",
"password": "123qwe!@"
}

```

# Directory structure

```
├-- ├── preface
│ │ ├── components
│ │ │ ├── Layout
│ │ │ ├── account
│ │ │ ├── accountDetail
│ │ │ │ └── hook
│ │ │ └── auth
│ │ │ └── hook
│ │ ├── lib
│ │ │ ├── api
│ │ │ │ └── instance
│ │ │ ├── assets
│ │ │ ├── constants
│ │ │ ├── data
│ │ │ ├── interfaces
│ │ │ ├── types
│ │ │ └── utils
│ │ ├── model
│ │ ├── pages
│ │ │ ├── account
│ │ │ ├── api
│ │ ├── public
│ │ ├── react-query
│ │ │ ├── hooks
│ │ ├── service
│ │ ├── styles
└-- └── server

```

Tried to group the folder structure with the most relevant ones.

- pages
    
    The Page folder contains only components that act as pages. Because nextJS routes to pages, it was consciously able to collect more pages.
    
- components
    
    Components are a collection of necessary components within the page. Although it has the disadvantage of being separated from the page, because the components are tied together, named the folder to make it easier to find.
    
    Hooks are included, but the hooks that are strongly combined with the components are tied into the components of each function.
    
- utils
    
    The utils were managed by including type, util function, global hook, and status.
    
- model
    
    A model is a collection of models of data coming from a server.
    

### Usage Library

- React-Query
    
    It was used to manage server status efficiently, distinguishing it from client status.
    
- cookies-next
    
    I used it to save the access token after successful login.
    
    I used it to manage cookies according to next.
    
- tailwindcss
    
    It was used to manage UI easily using class name.
    

# Demonstrated Video

![https://user-images.githubusercontent.com/97100045/202550478-eb9f4d19-87ec-4c57-94d5-3404f7d90da6.gif](https://user-images.githubusercontent.com/97100045/202550478-eb9f4d19-87ec-4c57-94d5-3404f7d90da6.gif)

![https://user-images.githubusercontent.com/50790145/202813248-c9295b1d-4eb5-4b4c-a418-643fa87f2723.gif](https://user-images.githubusercontent.com/50790145/202813248-c9295b1d-4eb5-4b4c-a418-643fa87f2723.gif)

![https://user-images.githubusercontent.com/97100045/202552356-201d50ae-6dcf-4921-8d6c-c3dbdc966190.gif](https://user-images.githubusercontent.com/97100045/202552356-201d50ae-6dcf-4921-8d6c-c3dbdc966190.gif)

# Implementation

## 1. Use NextJS Client Server and Cookies

- CORS issue was resolved using NextJS Client server. Because CORS is a browser issue, used the NEXTJS client server as a proxy server to solve CORS.
- The incoming accessToken was saved and used in the cookie. The advantage was that the client did not have to implement authorization because it was verified by the API server and redirected to login if there was no COOKIE.

## 2. Account list - Filtering, pageation, and search implementation

- Filtering was implemented using the query string of the URL as a state. When you reload, the URL in your browser remains intact, so the filtering value can remain the same.
- Page Nation was implemented by calculating the number of pages using the 'x-total-count' value in the response header.
- Implemented to change to page 1 when filtering conditions change.

## 3. Account details - Create and modify implementation

- Each function that changes the format is divided by function and put into the utils function to increase its reuse.
- Multiple values in constant were made into an array using Object.entries and each was modified with key value to reduce duplicate code.

# Troubleshooting

## 1. Hydration Error

- [Hydration failed because the initial UI does not match what was rendered on the server.](https://github.com/wanted-pre-onboarding-fe-7th-team-4/pre-onboarding-7th-3-2-4/issues/31)
- When using the SSR function in NextJS, a Hydration error occurred. We found that there was an error because there was a UI mismatch between the server and the client. The solution was eventually resolved by using useEffect instead of using SSR. See the issue for more information.

## 2. Many query string input parts

- After receiving params from the axiosConfig, the endpoint part receives only the path, and then the query string part is entered with the axios function to increase the readability of the code.

```
async getUserAccounts<TData>(
config?: AxiosRequestConfig
): Promise<AxiosResponse<TData>> {
const response = await this.api.get<TData>("accounts", {
...config
});

return response;
}

async () => {
await userService.searchUser<{ users: UserModel[] }>({ params: { id } }),
}

```

## 3. Implement the service to gracefully call the client api server and server-side api

When implementing the code, the amount of code needed to be written was higher because the server request had to be sent twice. However, I created the service by dividing our interests into authentication, authorization, account list inquiry, and user list inquiry. When making a request to the server, I created a service that can be used for both client api and server api Thanks to this, the development time could be further reduced because I only need to take the necessary parts from each part and use them.
