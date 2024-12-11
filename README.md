# splunk-logging
Analyze Realtime logs using splunk

Splunk
======
splunk is an extremely powerful platform that is
used to analyze data and logs produced by application

splunk allows you to monitor, search and analyze data and logs
through a web interface.

why splunk?
===========
Order Service

Inventory service

payment service 

if all logs capture by single log file
is not correct approach.

splunk segerate whole logs into seperate index.

create index: order_service_idx, inventory_service_idx,
payment_service_idx


Log4j, SL4j or util logger forward to splunk

log4j2-spring.xml

url: where your splunk server will redirect the logs
host: what is the host where your splunk server is running
token: what is the security token to connect with your splunk server
index: in which index you want to push your application logs
source: what is your source type(who will send your logs) log4j or json


$ wget https://download.splunk.com/products/splunk/releases/8.2.6/linux/splunk-8.2.6-a6fe1ee8894b-Linux-x86_64.tgz
$ ls
$ tar -zxvf splunk-8.2.6-a6fe1ee8894b-Linux-x86_64.tgz
$ clear
$ ls
$ cd bin
$ ls
$ ./splunk start --accept-license
$ administrator username: <uname>
password: <pwd>

1. cd splunk
2. cd bin
3. ./splunk start

The Splunk web interface is at http://ip-172-31-3-159:8000

settings -> data inputs-> local input-> http event collector go and verify
port number : 8088
copy token value: 507bd728-4c58-4c25-aac1-dac2e8f22cfb
copy source type: log4j
copy index : october
copy source: http-event-logs

splunk web interface

settings:
data inputs:
Http event collector->
global settings

all tokens enabled

default source type -> _json
default index-> main
default output group -> one
http port number: 8088

save

new token

name: order-service-logs
source name override: http-event-logs

next-> source type

new -> select -> log4j

go down
create a new index

index name: order_api_dev
in that enable reduction and reduction days as 5

save

select new indexname to selected items

review and click submit

Note: While creating index, 
index name as saravanan, index data type is events, data integrity check is enabled, max size is 500 GB, Max size of Hot is auto GB, Tsidx Retention policy is enabled
reduction, reduce Tsidx file older is 10 hrs

Note : While creating data inputs -> http event collector -> 
In global settings: All tokens - enabled, default source type is json, default index is default and port number is 8088

to verify the output:
Apps-> search and reporting:

New search:

index="october"

In postman : 

Post: localhost:9090/orders

Body -> raw -> json
{
  "id":21,
  "name": "soaps",
  "qty": 100,
  "price": 4500  
}

submit
ensure 200 ok

verify logs in console also.










