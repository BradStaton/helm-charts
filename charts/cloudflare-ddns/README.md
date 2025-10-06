# Cloudflare DDNS Helm Chart

This is a Helm chart for the [Cloudflare DDNS](https://github.com/favonia/cloudflare-ddns) project.

## Usage

You must create a [k8s secret](https://kubernetes.io/docs/concepts/configuration/secret/) in the namespace that this chart will deploy to.  The secret should container your Cloudflare API token in the `data.token` value.

```
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: cloudflare-api-token
  namespace: cloudflare-ddns
data:
  token: base64-encoded-cloudflare-api-token
```

This secret will be mounted at `/run/secrets/cloudlare_api_token` in the container.

## Parameters

You can customize values passed to the applicatoin by updating the values below.  For more information on these values, refer to [Cloudflare DDNS' Settings documentation](https://github.com/favonia/cloudflare-ddns?tab=readme-ov-file#%EF%B8%8F-all-settings)

| Parameter          | Description                                                  | Default            |
|--------------------|--------------------------------------------------------------|--------------------|
| domains            | The list of domains to update                                | []                 |
| ip4Domains         | List of domains for `A` records                              | []                 |
| ip6Domains         | List of domains for `AAAA` records                           | []                 |
| wafLists           | WAF lists to be managed                                      | []                 |
| ip4Provider        | IPv4 Address provider                                        | `cloudflare.trace` |
| ip6Provider        | IPv6 Address provider                                        | `cloudflare.trace` |
| cacheExpiration    | Expiration time for cached Cloudflare responses              | `6h0m0s`           |
| deleteOnStop       | Whether records should be deleted with the application exits | `false`            |
| timezone           | Timezone for logging and cron purposes                       | `UTC`              |
| updateCron         | Schedule for checking IPs and updating records               | `@every 5m`        |
| updateOnStart      | Whether to update immediately on application start           | `true`             |
| detectionTimeout   | Timeout for each attempt to detect IP address                | `5s`               |
| updateTime         | Timeout for each attempt to update DNS records               | `30s`              |
| proxied            | Whether DNS records should be proxied by Cloudflare          | `false`            |
| TTL                | Time-to-live of new DNS records                              | `1`                |
| recordComment      | Record comment of new DNS records                            | `""`               |
| wafListDescription | Text description of new WAF lists                            | `""`               |
| logEmojieEnabled   | Whether emojis will be used in logging                       | `true`             |
| quiet              | Whether logging should be reduced                            | `false`            |
| healthcheckPingUrl | Healtchecks ping URL to ping on successful updates           | `""`               |
| uptimeKumaUrl      | Uptime Kuma push URL to ping on successful updates           | `""`               |
| shoutrrrUrls       | List of shoutrrr URLs to notify of events                    | `""`               |