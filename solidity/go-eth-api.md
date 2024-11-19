#

https://geth.ethereum.org/docs/developers/dapp-developer/native

```

// create instance of ethclient and assign to cl
cl, err := ethclient.Dial("/tmp/geth.ipc")
if err != nil {
	panic(err)
}
_ = cl

// A simple starting point is to fetch the chain ID from the client. This e.g. is needed when signing a transaction as is to be seen in the next section
chainid, err := cl.ChainID(context.Background())
if err != nil {
    return err
}
```