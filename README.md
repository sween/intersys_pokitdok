intersys_pokitdok
=================

Interrogating the [ Pokitdok API ](https://platform.pokitdock.com) with Cache.

This is a small demonstration utility to interact and demonstrate the the Pokitdok API for v2.  The class is located on the asclepius server, instance HSPDV3, namespace HSEDGE1.

***Package HSPD.DSP.PokitDok.Client***

The first method to run does the oauth2 conversation to return an access token:

`   HSEDGE1>set token = ##class(HSPD.DSP.PokitDok.Client).Get()`

Check to make sure you have the token, as you will need it for the subsequent calls to the API.

    HSEDGE1>w token
    
    x6R4b6VzxQhqA9W4yEmg2dNFT0W8axoF5fLIaKer

For the interrogation we are going to be going after 3 resources on the API: Providers, Plan, and Payers.

        HSEDGE1>set providers = ##class(HSPD.DSP.PokitDok.Client).GetProviders(token)
        
        HSEDGE1>w providers
    98@%ZEN.proxyObject
    HSEDGE1>Do $System.OBJ.Dump(providers)
    +----------------- general information ---------------
    |      oref value: 98
    |      class name: %ZEN.proxyObject
    | reference count: 1
    +----------------- attribute values ------------------
    |           %changed = 1
    |      %data("data") = "97@%Library.ListOfObjects"
    |      %data("meta") = "55@%ZEN.proxyObject"
    |             %index = ""

You can walk down the objects and enumerate data like the following:

    HSEDGE1>w providers.data.GetAt(3).provider
    95@%ZEN.proxyObject
    HSEDGE1>w providers.data.GetAt(3).provider.npi
    1760485171

Here is the raw JSON output from the 3 Resources:

[See Produced Provider JSON From PokitDok](https://raw.githubusercontent.com/sween/intersys_pokitdok/master/example_pokitdok_providers.json)

[See Produced Plans JSON From PokitDok](https://raw.githubusercontent.com/sween/intersys_pokitdok/master/example_pokitdok_plans.json)

[See Produced Payers JSON From PokitDok](https://raw.githubusercontent.com/sween/intersys_pokitdok/master/example_pokitdok_payers.json)





        
