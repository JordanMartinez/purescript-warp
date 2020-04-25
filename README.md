# Warp

warp is a server library that wraps node's http library with an API inspired by the haskell version.   

## Installation

This is not yet published to pursuit. 
You can install this package by adding it to your packages.dhall:

```dhall
let additions =
  { purescript-warp =
       { dependencies =
          [ "node-fs-aff"
          , "node-net"
          , "node-url"
          , "wai"
          ]
       , repo =
           "https://github.com/Woody88/purescript-warp.git"
       , version =
           "master"
       }
  }
```
## Usage 

### Hello World 
```purescript 
import Prelude 

import Data.Tuple.Nested ((/\))
import Effect.Class.Console as Console 
import Network.Wai (responseStr, Application)
import Network.Warp.Run (runSettings)
import Network.Warp.Settings (defaultSettings)
import Network.HTTP.Types (status200)
import Network.HTTP.Types.Header (hContentType)

main :: Effect Unit
main = do 
    let beforeMainLoop = 
          Console.log $ "Listening on port " <> show defaultSettings.port
    runSettings defaultSettings app 

app :: Application
app req f = do
    f $ responseStr status200 [(hContentType /\ "text/plain")] "Hello World!"
```