# Check your Balance

1. Find out your principal id:

```
dfx identity get-principal
```

2. Save it somewhere.

e.g. My principal id is: lxsq6-dz5wg-3cdr3-4s2ed-tmulu-s6vm3-xs3pz-fn3y5-awcwp-55ke3-cae


3. Format and store it in a command line variable:
```
OWNER_PUBLIC_KEY="principal \"$( \dfx identity get-principal )\""
```

4. Check that step 3 worked by printing it out:
```
echo $OWNER_PUBLIC_KEY
```

5. Check the owner's balance:
```
dfx canister call token_backend balanceOf "( $OWNER_PUBLIC_KEY )"
```

# Charge the Canister


1. Check canister ID:
```
dfx canister id token_backend
```

2. Save canister ID into a command line variable:
```
CANISTER_PUBLIC_KEY="principal \"$( \dfx canister id token_backend )\""
```

3. Check canister ID has been successfully saved:
```
echo $CANISTER_PUBLIC_KEY
```

4. Transfer half a billion tokens to the canister Principal ID:
```
dfx canister call token_backend transfer "($CANISTER_PUBLIC_KEY, 500_000_000)"
```

# Deploy the Project to the Live IC Network

1. Create and deploy canisters:

```
dfx deploy --network ic
dfx deploy --playground
```

2. Check the live canister ID:
```
dfx canister --network ic id token_backend
dfx canister --network playground id token_backend
```

3. Save the live canister ID to a command line variable:
```
LIVE_CANISTER_KEY="principal \"$( \dfx canister --network ic id token_backend )\""
PG_CANISTER_KEY="principal \"$( \dfx canister --network playground id token_backend )\""
```

4. Check that it worked:
```
echo $LIVE_CANISTER_KEY
echo $PG_CANISTER_KEY
```

5. Transfer some token_backends to the live canister:
```
dfx canister --network ic call token_backend transfer "($LIVE_CANISTER_KEY, 50_000_000)"
dfx canister --network playground call token_backend transfer "($PG_CANISTER_KEY, 50_000_000)"
```

6. Get live canister front-end id:
```
dfx canister --network ic id token_backend_assets
dfx canister --network playground id token_backend_assets
```
7. Copy the id from step 6 and add .raw.ic0.app to the end to form a URL.
e.g. zdv65-7qaaa-aaaai-qibdq-cai.raw.ic0.app