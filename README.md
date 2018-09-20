# How to use the Chintai smart contract

The market is split into two types of orders: Stake Orders and Lease Orders.

Stake orders are for people with lots of EOS who want to make a profit.
Lease orders are for people who need more delegated bandwidth.

Both stake and lease orders can be made on Chintai by submitting a few actions to the chintai account.

## Making a stake order

To submit a stake order, the following actions have to be sent in the following order:

`cleos push action CHINTAI_ACCOUNT_NAME prepare '{"memo":"ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|RANDOM_STRING"}' -p YOUR_ACCOUNT_NAME`

`cleos transfer YOUR_ACCOUNT_NAME CHINTAI_ACCOUNT_NAME QUANTITY "ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|RANDOM_STRING"`

`cleos push action CHINTAI_ACCOUNT_NAME activate '{"memo":"ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|RANDOM_STRING"}' -p YOUR_ACCOUNT_NAME`

It is important that there is no white space and that the pipes are as shown above.
The side is a number, 0 for staking, 1 for leasing
The quantity must not include the currency symbol.
The interest rate is expressed as a number between 0 and 1.
The duration must be one of the predetermined market durations.
The random string is necessary to avoid problems with duplicate orders.
Below are some examples of stake orders:

A stake order for 500 EOS at an interest rate of 5% for a duration of 2 weeks:

`cleos push action chintaitest1 "myaccount|0|500|0.05|14|guiesbigu" -p myaccount`

`cleos transfer "myaccount" "chintaitest1" "500 EOS" "myaccount|0|500|0.05|14|guiesbigu"`

`cleos push action chintaitest1 "myaccount|0|500|0.05|14|guiesbigu" -p myaccount`


A stake order of 500000 EOS at an interest rate of 12% for a duration of 4 weeks:

`cleos push action chintaitest1 "myaccount|0|500000|0.12|14|sadsda" -p myaccount`

`cleos transfer "myaccount" "chintaitest1" "500000 EOS" "myaccount|0|500000|0.12|14|sadsda"`

`cleos push action chintaitest1 "myaccount|0|500000|0.12|14|sadsda" -p myaccount`

## Making a lease order

To submit a lease order, the following actions have to be sent in the following order:

`cleos push action CHINTAI_ACCOUNT_NAME prepare '{"memo":"ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|CPU_NET_RATIO|RANDOM_STRING"}' -p YOUR_ACCOUNT_NAME`

`cleos transfer YOUR_ACCOUNT_NAME CHINTAI_ACCOUNT_NAME QUANTITY "ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|CPU_NET_RATIO|RANDOM_STRING"`

`cleos push action CHINTAI_ACCOUNT_NAME activate '{"memo":"ACCOUNT_NAME|SIDE|QUANTITY|INTEREST_RATE|DURATION|CPU_NET_RATIO|RANDOM_STRING"}' -p YOUR_ACCOUNT_NAME`

It is important that the white spaces and pipe are as shown above.
The side is 0 for stake orders and 1 for lease orders.
The quantity is the quantity of EOS that you would like to receive.
The interest rate is expressed as a number between 0 and 1.
The duration must be one of the predetermined market durations.
The cpu-net-ratio is the fraction of the EOS you want dedicated to powering CPU.
The random string is necessary to avoid problems with duplicate orders.

Please note that if you submit orders manually, you have to make sure that your maths is correct for the memo, and the amount you transfer.

Below are some examples of lease orders:

A lease order for 100 EOS at a 1% interest rate for a duration of 2 weeks and with 80% of the tokens to be delegated to CPU:

`cleos push action chintaitest1 prepare '{"memo":"myaccount|1|100|0.01|14|0.8|egfsesbigu"}' -p myaccount`

`cleos transfer myaccount chintaitest1 "1 EOS" "myaccount|1|100|0.01|14|0.8|egfsesbigu"`

`cleos push action chintaitest1 activate '{"memo":"myaccount|1|100|0.01|14|0.8|egfsesbigu"}' -p myaccount`

A lease order for 500 EOS at a 5% interest rate for a duration of 1 week and with a 20% of tokens delegated to CPU:

`cleos push action chintaitest1 prepare '{"memo":"myaccount|1|500|0.05|7|0.2|safgasd"}' -p myaccount`

`cleos transfer myaccount chintaitest1 "25 EOS" "myaccount|1|500|0.05|7|0.2|safgasd"`

`cleos push action chintaitest1 activate '{"memo":"myaccount|1|500|0.05|7|0.2|safgasd"}' -p myaccount`

A lease order for 20000 EOS at a 2.5% interest rate for a duration of 4 weeks and with a 50-50 split between CPU and NET bandwidth:

`cleos push action chintaitest1 prepare '{"memo":"myaccount|1|20000|0.025|28|0.5|safadfads"}' -p myaccount`

`cleos transfer myaccount chintaitest1 "500 EOS" "myaccount|1|20000|0.025|28|0.5|safadfads"`

`cleos push action chintaitest1 activate '{"memo":"myaccount|1|20000|0.025|28|0.5|safadfads"}' -p myaccount`

## Cancelling an order

To cancel one of your orders, you must know the order ID.
Then the order can be cancelled by typing:

`cleos push action chintaitest1 cancelorder "ORDER_ID" -p myaccount`

For example, if I want to cancel order ID 42:

`cleos push action chintaitest1 cancelorder '{"id":"42"}' -p myaccount`
