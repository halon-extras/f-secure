## fsecure_atlant_scan(endpoint, tokenprovider, scan_settings, file, http_settings = [])

Scan a File pointer (file) with F-Secure Anti-virus (using the Atlant API).

**Params**

- endpoint `string` - the atlant endpoint base URL
- tokenprovider `function` - the token provider (see `fsecure_tokenprovider` function)
- scan_settings `array` - the atlant API scan settings
- fp `File` - a file object
- http_settings `array` - http options (passed to `http` function)

**Returns**: an array with ``scan_result`` and optionally ``detections`` (see Atlant API documentation), or an array with an ``error`` (produced by this client).

## fsecure_tokenprovider(endpoint, client_id, client_secret, http_settings = [])

Return a token provider to be used with the `fsecure_atlant_scan` function.

**Params**

- endpoint `string` - the authorization endpoint base URL
- client_id `string` - the client id
- client_secret `string` - the client secret
- http_settings `array` - http options (passed to http() function)

## Example

The following sample will trigger the EICAR detection.

```
$tokenprovider = fsecure_tokenprovider(
	"https://10.2.50.38:8081",
	"...",
	"...",
	[
		"tls_verify_peer" => false,
	]);
echo fsecure_atlant_scan(
	"https://10.2.50.38:8083",
	$tokenprovider,
	[
		"scan_settings" => [
		]
	],
	File::String(''X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*''),
	[
		"tls_verify_peer" => false,
	]
);
```
