# Intro

## Read uncommitted

## Read committed (default Isolation Level)

## Repeatable Read

## Serializable (highest level)

## Deadlock workaround

- Using `READ-UNCOMMITTED` at Context Level
- Use `Read uncommitted` at the transaction level
- Using `Retry failures` of entity framework
- Store Procedure with a `NOLOCK` Query
- Stored Procedure is called from `Entity Framework`
- SQL View with a `NOLOCK` query
- Get records were dealdlocks and kill these processes in sql server 
## References:

- https://www.c-sharpcorner.com/UploadFile/ff2f08/prevent-dead-lock-in-entity-framework/
