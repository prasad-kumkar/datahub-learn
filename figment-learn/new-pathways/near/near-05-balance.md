After the creation of your account on the **NEAR** testnet, the Helper provides an automatic **airdrop** of 200 **NEAR** tokens. Here, we're going to check the balance of our account to make sure everything went alright.

------------------------

# Challenge

{% hint style="tip" %}
In `pages/api/near/balance.ts`, complete the code of the default function.
{% endhint %}

**Take a few minutes to figure this out**

```typescript
  try {
      const { network, accountId } = req.body;
      const config = configFromNetwork(network);       
      const client = await connect(config);
      const account = undefined;
      const balance = undefined;
      console.log(balance)
      return res.status(200).json(balance)
  }
```

**Need some help?** Check out these links
* [Basic `NEAR` economics](https://docs.near.org/docs/concepts/gas)
* [The `Account` class](https://near.github.io/near-api-js/classes/account.account-1.html)

{% hint style="info" %}
[You can **join us on Discord**, if you have questions](https://discord.gg/fszyM7K)
{% endhint %}

Still not sure how to do this? No problem! The solution is below so you don't get stuck.

------------------------

# Solution

```typescript
  try {
      const { network, accountId } = req.body;
      const config = configFromNetwork(network);       
      const client = await connect(config);
      const account = await client.account(accountId);
      const balance = await account.getAccountBalance();
      console.log(balance)
      return res.status(200).json(balance)
  }
```

**What happened in the code above?**
* First, we create an `account` object, representing our account. Pass the `accountId` as the only argument.
* Next, we call the `getAccountBalance()` method, which returns the calculated account balance. The `AccountBalance` type has four properties; `total`, `stateStaked`, `staked` and `available`. A calculated balance might contain some staked NEAR tokens, but right now we haven't got anything staked so don't worry about this.

{% hint style="tip" %}
The amount returned by `getAccountBalance()` is denominated in **yoctoNEAR**, so to convert it to **NEAR** you'll need to divide it by 10**24 
{% endhint %}


------------------------

# Make sure it works

Once the code is complete and the file is saved, Next.js will rebuild the API route. Click on **Check Balance** and you should see the balance displayed on the page:

![](../../../.gitbook/assets/pathways/near/near-balance.gif)

-----------------------------

# Next

200 **NEAR** available, hmmm ... I guess it's more than enough to do our first transfer. In the next step, we're going to buy a pizza!
