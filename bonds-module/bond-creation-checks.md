# Bonds Module Bond Creation Checks

## BondDid
- Not blank
- Must match regex `did:(ixo:|sov:)([a-zA-Z0-9]){21,22}([/][a-zA-Z0-9:]+|)`, meaning:
  - With prefix `did:ixo:` or `did:sov:`
  - Followed by 21 or 22 alphanumeric characters
  - Optionally followed by `/` and alphanumeric characters

## Token
- Not blank
- Must match regex `[a-z][a-z0-9]{2,15}`, meaning:
    - alphanumeric
    - starting with a letter
    - of length between 2 and 15

## Name
- Not blank

## Description
- Not blank

## CreatorDid
- Not blank
- Must match regex `did:(ixo:|sov:)([a-zA-Z0-9]){21,22}([/][a-zA-Z0-9:]+|)`, meaning:
  - With prefix `did:ixo:` or `did:sov:`
  - Followed by 21 or 22 alphanumeric characters
  - Optionally followed by `/` and alphanumeric characters

## FunctionType
- Not blank
- Must be one of: `power_function`, `sigmoid_function`, `swapper_function`, `augmented_function`

## FunctionParameters
- Can be blank for some function types (more info below)
- No negative numbers
- Includes all required params for the particular function
  - power function: `n`, `m`, `c`
  - sigmoid function: `a`, `b`, `c`
  - swapper function: no params
  - augmented function: `d0`, `p0`, `theta`, `kappa`
- No extra or missing parameters
- Extra function type dependent restrictions
  - power function: `n` must be an integer (no decimal point)
  - sigmoid function: `c` cannot be zero
  - swapper function: no extra checks
  - augmented function:
    - `d0` and `kappa` must be an integer (no decimal point)
    - `d0`, `theta`, and `kappa` cannot be zero
    - `theta` must be strictly less than 1

## ReserveTokens
- Not blank
- Reserve token names must all match same regex as [`Token`](#token)
- There cannot be duplicate reserve tokens
- Number of reserve tokens depends on function type:
  - swapper function: 2 reserve tokens
  - other functions: any number of reserve tokens
- None of the reserve tokens can be the same as the [`Token`](#token)

## TxFeePercentage
- Not blank
- Must be a valid number (e.g. 20.5)
- Cannot be negative
- When added to [`ExitFeePercentage`](#ExitFeePercentage), cannot add up to 100

## ExitFeePercentage
- Not blank
- Must be a valid number (e.g. 20.5)
- Cannot be negative
- When added to [`TxFeePercentage`](#TxFeePercentage), cannot add up to 100

## FeeAddress
- Not blank
- Must be a valid ixo address (e.g. `ixo107pmtx9wyndup8f9lgj6d7dnfq5kuf3sapg0vx`)

## MaxSupply
- Not blank
- Has to be a valid coin value (e.g. 10000uixo)
- Token name has to match [`Token`](#Token)
- Amount cannot be zero

## OrderQuantityLimits
- Can be blank, implying no limits
- Can include more than one denomination of coins
- Has to be a valid coins value (e.g. 10000uixo)

## SanityRate
- Not blank
- Must be a valid number (`1`, `2.5`, ... etc)
- Cannot be negative

## SanityMarginPercentage
- Not blank
- Must be a valid number (`1`, `2.5`, ... etc)
- Cannot be negative

## AllowSells
- Not blank
- Must be a valid boolean (`true` or `false`)

## BatchBlocks
- Not blank
- Must be a valid integer (`1`, `2`, ... etc)
- Cannot be zero

## OutcomePayment
- Can be blank, implying no outcome payment
- Can include more than one denomination
- Has to be a valid coins value (e.g. 10000uixo,20000abc)

## Further general later-stage checks
- Bond cannot already exist (checked using [`BondDid`](#BondDid))
- Bond token cannot already be used (checked using [`Token`](#Token))
- Bond token cannot be the staking token (`uixo` in the case of ixo)
