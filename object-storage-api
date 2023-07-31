## API for object storage browser

### 1) createBucket
---
##### Method `POST`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/bucket/{bucket-name}
```
##### Return value:
- `201`: bucket name
- `500`: error message

### 2) listBuckets
---
##### Method `GET`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/buckets
```
##### Return value:
- `200`: list of buckets in body:

`example:`
```json
[
    {
        "name": "nxxxxxt",
        "creation_date": "2023-07-13T07:01:26.049Z",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt"
    },
    {
        "name": "test1",
        "creation_date": "2023-06-25T19:48:02.565Z",
        "visibility": "private",
        "url": ""
    },
    {
        "name": "test2",
        "creation_date": "2023-07-04T17:17:49.398Z",
        "visibility": "custom",
        "url": ""
    }
]
```
- `500`: error message

### 3) getBucket
---
##### Method `GET`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/buckets/{bucket-name}
```
##### Return value:
- `200`: buckets detail in body:

`example:`
```json
{
    "name": "nxxxxxt",
    "creation_date": "2023-07-13T07:01:26.049Z",
    "visibility": "public",
    "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt"
}
```
- `500`: error message

### 4) removeBucket
---
##### Method `DELETE`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/buckets/{bucket-name}
```
##### Return value:
- `200`
- `500`: error message

### 5) removeFullBucket
---
##### Method `DELETE`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/buckets/{bucket-name}/force
```
##### Return value:
- `200`
- `500`: error messages in body:

`example:`
```json
[
    "The specified bucket does not exist."
]
```
### 6) listFiles
---
##### Method `GET`
##### Path:
```json
/{proj-id}/credentials/{cred-id}/buckets/{bucket-name}/files
```
##### Optional querry param:

`prefix` string

`example:`
```json
/{proj-id}/credentials/{cred-id}/buckets/{bucket-name}/files?prefix=Folder/
```
##### Return value:
- `200`: list of objects in bucket:

`example without prefix param:`
```json
[
    {
        "name": "Folder/",
        "last_modified": "2023-07-31T20:21:02.089Z",
        "size": 0,
        "owner": "8xxxxxxxxxxxxxxxxxxxxxxxxxxx2",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt/Folder/"
    },
    {
        "name": "Folder/test2.zip",
        "last_modified": "2023-07-31T20:26:31.162Z",
        "size": 8466306,
        "owner": "8xxxxxxxxxxxxxxxxxxxxxxxxxxx2",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt/Folder/test2.zip"
    },
    {
        "name": "test21.zip",
        "last_modified": "2023-07-18T15:08:25.162Z",
        "size": 8466306,
        "owner": "8xxxxxxxxxxxxxxxxxxxxxxxxxxx2",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt/test21.zip"
    }
]
```
`example with prefix=Folder/ param:`
```json
[
    {
        "name": "Folder/",
        "last_modified": "2023-07-31T20:21:02.089Z",
        "size": 0,
        "owner": "8xxxxxxxxxxxxxxxxxxxxxxxxxxx2",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt/Folder/"
    },
    {
        "name": "Folder/test2.zip",
        "last_modified": "2023-07-31T20:26:31.162Z",
        "size": 8466306,
        "owner": "8xxxxxxxxxxxxxxxxxxxxxxxxxxx2",
        "visibility": "public",
        "url": "https://uxxxxxxxxxxxxxxxxxxxxxd.eu:8080/8xxxxxxxxxxxxxxxxxxxxxxxxxxx2:nxxxxxt/Folder/test2.zip"
    }
]
```
- `500`: error message
