# Problem API V1

[WIP]

## GET `/api/v1/problem`

[WIP]

## POST `/api/v1/problem`

Should wait package to be put.

## PUT `/api/v1/problem/:problem-slug/package`

Replace/put the problem package in S3 storage,
mark the problem as package uploaded.

## POST `/api/v1/problem/:problem-slug/judge`

Check problem is package uploaded,
then send judge task to Judger.
