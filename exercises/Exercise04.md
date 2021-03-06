```haskell
module Exercise04 where

import ClassyPrelude
import Data.Aeson (decode, encode)
import Test.Hspec (Spec, describe, hspec, shouldBe, shouldSatisfy)
import Test.Hspec.QuickCheck (prop)
import Test.QuickCheck (Arbitrary, arbitrary, elements)

import Solved.Exercise03
```

Now, let's write some tests so that we can do this once and we never have to think about it ever again, even when we
refactor. We create a new enumeration, generate the instances, and test the instances. That way we're testing that (1)
the template haskell even compiles, because that would be terrible if it didn't, and (2) that the generated code does
what we want whenever we generate the way we expect.

```haskell
data Fantastic
  = FantasticMrFox
  | FantasticBeasts
  | FantasticFantasia
  deriving (Eq, Show)

data Incorrect
  = Correct
  deriving (Eq, Show)

deriveEnumInstances ''Fantastic

instance Arbitrary Fantastic where
  arbitrary = elements [FantasticMrFox, FantasticBeasts, FantasticFantasia]
```

## Exercises

### Write tests for the instances we derived

```haskell
-- |Fill in the spec bodies with the tests we want to run.
thEnumSpec :: Spec
thEnumSpec = describe "TH Enums" $ do
  prop "always round trips JSON instances" $ \ (x :: Fantastic) ->
    fail "TODO fill me in" :: IO ()

  prop "always encodes to something we expect" $ \ (x :: Fantastic) ->
    fail "TODO fill me in" :: IO ()
```

## Testing

```bash
stack ghci
:l exercises/Exercise06.md
hspec thEnumSpec
```
