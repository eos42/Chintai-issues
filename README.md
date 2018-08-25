# How to use the Chintai smart contract

The market is split into two types of orders: Stake Orders and Lease Orders.

Stake orders are for people with lots of EOS who want to make a profit.
Lease orders are for people who need more delegated bandwidth.

Both stake and lease orders can be made on Chintai by making a transfer to the chintai account.

## Making a stake order

To submit a stake order, the memo must be correctly formatted for the transfer as follows:

stake | QUANTITY | INTEREST_RATE | DURATION | RANDOM_STRING

It is important that the white spaces and pipes are as shown above.
The quantity must include the currency.
The interest rate is expressed as a number between 0 and 1.
The duration must be one of the predetermined market durations.
The random string is necessary to avoid problems with duplicate orders.
Below are some examples of stake orders:

A stake order for 500 EOS at an interest rate of 5% for a duration of 2 weeks:

`cleos transfer "myaccount" "chintaitest1" "500 EOS" "stake | 500 EOS | 0.05 | 14 | guiesbigu"`

A stake order for 123.4567 EOS at an interest rate of 1.23% for a duration of 1 week:

`cleos transfer "myaccount" "chintaitest1" "123.4567 EOS" "stake | 123.4567 EOS | 0.0123 | 7 | rgndioun"`

A stake order of 500000 EOS at an interest rate of 12% for a duration of 1 year:

`cleos transfer "myaccount" "chintaitest1" "500000 EOS" "stake | 500000 EOS | 0.12 | 365 | hguer8g"`

## Making a lease order

To submit a lease order, the memo must be correctly formatted for the transfer as follows:

lease | QUANTITY_TO_LEASE | INTERST_RATE | DURATION | CPU_NET_RATIO | RANDOM_STRING

It is important that the white spaces and pipe are as shown above.
The quantity is the quantity of EOS that you would like to receive.
The interest rate is expressed as a number between 0 and 1.
The duration must be one of the predetermined market durations.
The cpu-net-ratio is the fraction of the EOS you want dedicated to powering CPU.
The random string is necessary to avoid problems with duplicate orders.

Please note that if you submit orders manually, you have to make sure that your maths is correct for the memo, and the amount you transfer.

Below are some examples of lease orders:

A lease order for 100 EOS at a 1% interest rate for a duration of 2 weeks and with 80% of the tokens to be delegated to CPU:

`cleos transfer "myaccount" "chintaitest1" "1 EOS" "lease | 100 EOS | 0.01 | 14 | 0.8 | egfsesbigu"`

A lease order for 500 EOS at a 5% interest rate for a duration of 1 week and with a 20% of tokens delegated to CPU:

`cleos transfer "myaccount" "chintaitest1" "25 EOS" "lease | 500 EOS | 0.05 | 7 | 0.2 | egsegsggu"`

A lease order for 20000 EOS at a 2.5% interest rate for a duration of 1 year and with a 50-50 split between CPU and NET bandwidth:

`cleos transfer "myaccount" "chintaitest1" "500 EOS" "lease | 20000 EOS | 0.025 | 365 | 0.5 | g76vff5rfv"`


## Cancelling an order

To cancel one of your orders, you must know the order ID.
Then the order can be cancelled by typing:

`cleos push action chintaitest1 cancelorder "ORDER_ID" -p myaccount`

For example, if I want to cancel order ID 42:

`cleos push action chintaitest1 cancelorder "42" -p myaccount`
