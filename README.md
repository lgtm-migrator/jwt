# JWT



A simple JWT decoder.

## Usage

### Parsing URLs

```go
func ExampleParseURL() {
	u := "https://jwt.ms/?state=d61b0af6-4704-4070-b854-ee5feab01bf2&access_token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTQ1ODY5ODIsIm5iZiI6MTYxNDU4MzM4MiwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9nb2xsYWhhbGxpYXV0aC5iMmNsb2dpbi5jb20vNDkyMDY1NmQtMzZlMC00YjM1LTg5NGQtMGEwYTE0YmVjOGIzL3YyLjAvIiwic3ViIjoiNzYyNWY0MDktMWZhNy00ZDc4LTkzYjAtNWMzNDAyNTVjZGYyIiwiYXVkIjoiMTIzNDU2Nzg5Iiwibm9uY2UiOiJkZWZhdWx0Tm9uY2UiLCJpYXQiOjE2MTQ1ODMzODIsImF1dGhfdGltZSI6MTYxNDU4MzM4Miwib2lkIjoic29tZS1vaWQiLCJnaXZlbl9uYW1lIjoiQWtzaGF5IiwiZmFtaWx5X25hbWUiOiJHb2xsYWhhbGxpIiwidGZwIjoiQjJDXzFfU2lnblVwU2lnbkluRmxvdyJ9.CNbe3qUhpUR7U51e9k1miAdQP3ZEbCDip67MlvgTpFsFmB3nbjp7wi8e-66cPoS9z_hmQP3wLc5I8KE-b4_cFCzHZkhuQPA0Mhi9mBAZ_tAPSXNaDeiX1FEalsiH_sWuHWnojxSwlSxeKL9Tlh_0u5vXaABILdDeRWOTBJDHZ5I2BgIk8J_hI-fXDvBb0wfjI4mQe7lQqDZLVos4mlA1Uhpz2wN7Lorc31PZo02STbk5S1j1BMk4eQUS_OHTKZfAlUmfV9giWEMr7qk21eSy_HlybVKQgCB9Cde_rmNWJETyw6X712QGYWaDkDrwocQ99wR6rALWVkkTOhmL6CRT5Q&token_type=Bearer&expires_in=3600&code=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTQ1ODY5ODIsIm5iZiI6MTYxNDU4MzM4MiwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9nb2xsYWhhbGxpYXV0aC5iMmNsb2dpbi5jb20vNDkyMDY1NmQtMzZlMC00YjM1LTg5NGQtMGEwYTE0YmVjOGIzL3YyLjAvIiwic3ViIjoiNzYyNWY0MDktMWZhNy00ZDc4LTkzYjAtNWMzNDAyNTVjZGYyIiwiYXVkIjoiMTIzNDU2Nzg5Iiwibm9uY2UiOiJkZWZhdWx0Tm9uY2UiLCJpYXQiOjE2MTQ1ODMzODIsImF1dGhfdGltZSI6MTYxNDU4MzM4Miwib2lkIjoic29tZS1vaWQiLCJnaXZlbl9uYW1lIjoiQWtzaGF5IiwiZmFtaWx5X25hbWUiOiJHb2xsYWhhbGxpIiwidGZwIjoiQjJDXzFfU2lnblVwU2lnbkluRmxvdyJ9.CNbe3qUhpUR7U51e9k1miAdQP3ZEbCDip67MlvgTpFsFmB3nbjp7wi8e-66cPoS9z_hmQP3wLc5I8KE-b4_cFCzHZkhuQPA0Mhi9mBAZ_tAPSXNaDeiX1FEalsiH_sWuHWnojxSwlSxeKL9Tlh_0u5vXaABILdDeRWOTBJDHZ5I2BgIk8J_hI-fXDvBb0wfjI4mQe7lQqDZLVos4mlA1Uhpz2wN7Lorc31PZo02STbk5S1j1BMk4eQUS_OHTKZfAlUmfV9giWEMr7qk21eSy_HlybVKQgCB9Cde_rmNWJETyw6X712QGYWaDkDrwocQ99wR6rALWVkkTOhmL6CRT5Q&id_token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTQ1ODY5ODIsIm5iZiI6MTYxNDU4MzM4MiwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9nb2xsYWhhbGxpYXV0aC5iMmNsb2dpbi5jb20vNDkyMDY1NmQtMzZlMC00YjM1LTg5NGQtMGEwYTE0YmVjOGIzL3YyLjAvIiwic3ViIjoiNzYyNWY0MDktMWZhNy00ZDc4LTkzYjAtNWMzNDAyNTVjZGYyIiwiYXVkIjoiMTIzNDU2Nzg5Iiwibm9uY2UiOiJkZWZhdWx0Tm9uY2UiLCJpYXQiOjE2MTQ1ODMzODIsImF1dGhfdGltZSI6MTYxNDU4MzM4Miwib2lkIjoic29tZS1vaWQiLCJnaXZlbl9uYW1lIjoiQWtzaGF5IiwiZmFtaWx5X25hbWUiOiJHb2xsYWhhbGxpIiwidGZwIjoiQjJDXzFfU2lnblVwU2lnbkluRmxvdyJ9.CNbe3qUhpUR7U51e9k1miAdQP3ZEbCDip67MlvgTpFsFmB3nbjp7wi8e-66cPoS9z_hmQP3wLc5I8KE-b4_cFCzHZkhuQPA0Mhi9mBAZ_tAPSXNaDeiX1FEalsiH_sWuHWnojxSwlSxeKL9Tlh_0u5vXaABILdDeRWOTBJDHZ5I2BgIk8J_hI-fXDvBb0wfjI4mQe7lQqDZLVos4mlA1Uhpz2wN7Lorc31PZo02STbk5S1j1BMk4eQUS_OHTKZfAlUmfV9giWEMr7qk21eSy_HlybVKQgCB9Cde_rmNWJETyw6X712QGYWaDkDrwocQ99wR6rALWVkkTOhmL6CRT5Q"
	c := "123456789"
	var data providers.AzureB2C
	token, err := ParseURL(u, c)
	if err != nil {
		panic(err)
	}
	err = token.UnmarshalAccessToken(&data)
	if err != nil {
		panic(err)
	}
	fmt.Println(data)
	// Output: {1614586982 1614583382 1.0 https://gollahalliauth.b2clogin.com/4920656d-36e0-4b35-894d-0a0a14bec8b3/v2.0/ 7625f409-1fa7-4d78-93b0-5c340255cdf2 123456789 defaultNonce 1614583382 1614583382 some-oid Akshay Gollahalli B2C_1_SignUpSignInFlow    }
}
```

### Parsing Tokens

```go
func ExampleParseAccessToken() {
	u := "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE2MTQ1ODY5ODIsIm5iZiI6MTYxNDU4MzM4MiwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9nb2xsYWhhbGxpYXV0aC5iMmNsb2dpbi5jb20vNDkyMDY1NmQtMzZlMC00YjM1LTg5NGQtMGEwYTE0YmVjOGIzL3YyLjAvIiwic3ViIjoiNzYyNWY0MDktMWZhNy00ZDc4LTkzYjAtNWMzNDAyNTVjZGYyIiwiYXVkIjoiMTIzNDU2Nzg5Iiwibm9uY2UiOiJkZWZhdWx0Tm9uY2UiLCJpYXQiOjE2MTQ1ODMzODIsImF1dGhfdGltZSI6MTYxNDU4MzM4Miwib2lkIjoic29tZS1vaWQiLCJnaXZlbl9uYW1lIjoiQWtzaGF5IiwiZmFtaWx5X25hbWUiOiJHb2xsYWhhbGxpIiwidGZwIjoiQjJDXzFfU2lnblVwU2lnbkluRmxvdyJ9.CNbe3qUhpUR7U51e9k1miAdQP3ZEbCDip67MlvgTpFsFmB3nbjp7wi8e-66cPoS9z_hmQP3wLc5I8KE-b4_cFCzHZkhuQPA0Mhi9mBAZ_tAPSXNaDeiX1FEalsiH_sWuHWnojxSwlSxeKL9Tlh_0u5vXaABILdDeRWOTBJDHZ5I2BgIk8J_hI-fXDvBb0wfjI4mQe7lQqDZLVos4mlA1Uhpz2wN7Lorc31PZo02STbk5S1j1BMk4eQUS_OHTKZfAlUmfV9giWEMr7qk21eSy_HlybVKQgCB9Cde_rmNWJETyw6X712QGYWaDkDrwocQ99wR6rALWVkkTOhmL6CRT5Q"
	c := "123456789"
	var data providers.AzureB2C
	token := ParseAccessToken(u, c)
	err := token.UnmarshalAccessToken(&data)
	if err != nil {
		panic(err)
	}
	fmt.Println(data)
	// Output: {1614586982 1614583382 1.0 https://gollahalliauth.b2clogin.com/4920656d-36e0-4b35-894d-0a0a14bec8b3/v2.0/ 7625f409-1fa7-4d78-93b0-5c340255cdf2 123456789 defaultNonce 1614583382 1614583382 some-oid Akshay Gollahalli B2C_1_SignUpSignInFlow    }
}
```

## Security

There is a minimal security validation in this module. Use it at your own risk. I suggest using [https://github.com/dgrijalva/jwt-go](https://github.com/dgrijalva/jwt-go) for secure validation of your token.
