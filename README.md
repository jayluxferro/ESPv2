## ESPv2 JWT authentication bypass via `X-HTTP-Method-Override` header

This BurpSuite extension tests ESPv2 malicious X-HTTP-Method-Override header value to bypass JWT authentication in specific cases.

### CVE-2023-30845

ESPv2 is a service proxy that provides API management capabilities using Google Service Infrastructure. ESPv2 2.20.0 through 2.42.0 contains an authentication bypass vulnerability. API clients can craft a malicious `X-HTTP-Method-Override` header value to bypass JWT authentication in specific cases. ESPv2 allows malicious requests to bypass authentication if both the conditions are true: The requested HTTP method is **not** in the API service definition (OpenAPI spec or gRPC `google.api.http` proto annotations, and the specified `X-HTTP-Method-Override` is a valid HTTP method in the API service definition. ESPv2 will forward the request to your backend without checking the JWT. Attackers can craft requests with a malicious `X-HTTP-Method-Override` value that allows them to bypass specifying JWTs. Restricting API access with API keys works as intended and is not affected by this vulnerability. Upgrade deployments to release v2.43.0 or higher to receive a patch. This release ensures that JWT authentication occurs, even when the caller specifies `x-http-method-override`. `x-http-method-override` is still supported by v2.43.0+. API clients can continue sending this header to ESPv2.

### Details
1. https://github.com/GoogleCloudPlatform/esp-v2/security/advisories/GHSA-6qmp-9p95-fc5f
2. https://cve.circl.lu/cve/CVE-2023-30845