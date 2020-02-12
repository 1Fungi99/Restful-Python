# Restful-Python

# Device Registry Service

All responses will have the form

```json
{
    "data": "mixed type holding the contend of the response",
    "message": "description of what happened
}
```

Subsequent response definition will only detal the expected value of the 'data field'

### List all devices

**Definition**
'GET/devices'

**Response**

- '200 OK' on success

```json
[
  {
    "identifier": "floor-lamp",
    "name": "Floor Lamp",
    "device": "switch",
    "controller_gateway": "192.1.68.0.2"
  },
  {
    "identifier": "samsung-tv",
    "name": "Living Room TV",
    "controller_gateway": "192.168.0.9"
  }
]
```

## Registration

`POST /devices`

**Arguments**

- `"identifier": string` a globally unique identifier for this device
- `"name":string` a friendly name for this device
- `"device_type":string` the type of device as understood by client
- `"controller_gateway":string` the IP address of the device's controller

If a device with the given identifier already exists, the existing device will be overwritten

**Response**

-`201 Created`

```json
{
  "identifier": "floor-lamp",
  "name": "Floor Lamp",
  "device": "switch",
  "controller_gateway": "192.1.68.0.2"
}
```

## Lookup device details

`GET /device/<identifier>`

**Response**

- `400 Not Found` if the device does not exist
- `200 OK` on success

```json
{
  "identifier": "floor-lamp",
  "name": "Floor Lamp",
  "device": "switch",
  "controller_gateway": "192.1.68.0.2"
}
```

## Delete a device

**Definition**

`DELETE /devices/<identifier>`

**Response**

- `400 Not Found` if the device does not exist
- `204 No Content` no useful data to return
