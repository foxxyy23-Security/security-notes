# SentinelOne API Quick Start

**Common endpoints and Python snippets for automation.**

## Authentication
Headers required for all requests.

```python
headers = {
    "Authorization": "ApiToken <YOUR_API_TOKEN>",
    "Content-Type": "application/json"
}
base_url = "https://usea1-001.sentinelone.net/web/api/v2.1"
```

## Get Agent Info
Retrieve details for a specific endpoint by hostname.

```python
def get_agent_id(hostname):
    params = {
        "computerName": hostname,
        "isActive": True
    }
    response = requests.get(f"{base_url}/agents", headers=headers, params=params)
    return response.json()['data'][0]['id']
```

## Isolate Endpoint
**Warning:** This disconnects the host from the network.

```python
def isolate_host(agent_id):
    payload = {
        "filter": {
            "ids": [agent_id]
        }
    }
    response = requests.post(f"{base_url}/agents/actions/disconnect", headers=headers, json=payload)
    return response.status_code
```

## Fetch Threat Notes
Get analyst notes attached to a specific threat ID.

```
GET /threats/{threat_id}/notes
# Useful for syncing S1 notes to Jira/ServiceNow
```
