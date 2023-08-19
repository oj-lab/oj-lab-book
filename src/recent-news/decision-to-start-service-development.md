# Decision to Start Service Development

In the past few months,
we all aims to build the most essentail part of an online judge system:
The judge machine.

But recently I found it's really difficult to decide
which functionality the service will be needed for the judger.

So we decide to restart the development of oj-lab-service,
to find out what functionalities we will need in the future.

## Milestones

- Development environment prepare (Including installation guide)
  - Golang
  - Postgres (Dev container + Ways to setup and clean datas)
  - S3 Proxy (Store problem packages)
- Problem manage service implementation
  - APIs to import problem packages (Store in S3 and DB)
