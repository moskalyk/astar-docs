---
sidebar_position: 4
---

# Collections

Astar Studio offers the ability to manage Collections of collectible metadata, including: collectible details, images, and properties. Within the Studio, Collections can be linked to deployable contracts from the Studio for easy crafting flows.

Media and metadata is saved to [Google Cloud](https://cloud.google.com/) servers (replicated across the United States) where certain functionality allows you to have control over updates and public / private viewing of your collection information.

The following functions are possible:

1. [Create Collection](./manage_collections.md#1-create-a-collection): Create a new collection and specify details
2. [Link a Contract](./manage_collections.md#2-link-a-contract):  Deploy and link a contract
3. [Create Collectible](./manage_collections.md#3-create-a-collectible): Upload media artwork as an image and encode properties
4. [Upate Settings](./manage_collections.md#4-update-info-in-settings): Update collection details in settings
5. [(Optional) Reference Metadata Token URIs](./manage_collections.md#5-reference-metadata-token-uri): Reference token metadata base URI for any collectible contract

## 1. Create a Collection

First navigate to your project from the top left hand drop down of [Astar Studio](https://studio.astar.network/) and select the `Collections` page view from the left nav, then select the `+ Create a collection`

![create collection](img/collections/studio_create_collection.png)

Then input your details for the collection, like `Collection Name`, `Description` for the contract info, `Collection Data` being `Visible (Public)` or `Private (Hidden)` where for the data to be viewable select Visible (Public), and include your projects `External Link` to a website.

![add details to collection](img/collections/studio_create_collection_input_details.png)

## 2. Link a Contract

After a collection has been created you can first link a contract by deploying a collectible contract (i.e. `ERC1155` or `ERC721`) and having the `baseMetadataURI` being set on the deployment by selecting the `+ Link contract`

![link a contract](img/collections/studio_collections_link_contract.png)

Then select the `+ Deploy new contract`

![deploy a contract](img/collections/studio_collections_deploy_contract.png)

Select your contract type or upload your own 

![contract type](img/collections/studio_select_contract_type.png)

And complete your contract details, specifying the `Network`, `Contract Name`, and `Royalties`, and finally select `Deploy Contract` to then complete the transaction signing in the Wallet popup.

![contract details](img/collections/studio_deploy_contract_details.png)

Then you will notice if you check out the `Read Contract` section tab of the contract, if you `Read` from the `baseURI` it will show you the metadata url for where when read from the Indexer, `<token_id>.json` will get appended to the end to reference the json for the collectible.

![read base uri](img/collections/studio_read_base_uri.png)

## 3. Create a Collectible

In order to create a Collectible as part of the Collection, return to the `Collections` page and select the `+ Add a collectible`

![add a collectible](img/collections/studio_collections_add_a_collectible.png)

Then update the details like `Collectible Name` and `Description`, then upload your artwork by selecting the greyish field 

![update collectible details](img/collections/studio_collections_update_art_and_details.png)

#### Add a metadata property

You can also add certain properties to your collectible, by selecting the `+ Add a property` which can be useful for inscribing more information like numbers or strings when using the metadata in any game.

![add a property](img/collections/studio_collection_add_property.png)

Assigning the key and value to each property

![asign properties](img/collections/studio_collections_assign_properties.png)

Complete the prior steps until you get your final result of a collectible added to a collection

![final result of collectible added](img/collections/studio_collections_final_result_of_collectible.png)

## 4. Update Info in Settings

At any point you can update the details for your collectible in the settings

![settings](img/collections/studio_collections_access_settings.png)

Once in settings, you can update any one of the information fields, like: `Collection Name`, `Description`, visibility of `Collection data`, and an `External Link` to reference a website on the web.

![settings](img/collections/studio_collections_update_info.png)

#### Delete Collection Data

You can delete all of the Collection data for the contract by selecting `Delete collection data` which will permanently delete data all data, an action that cannot be undone.

## 5. Reference Metadata Token URI

Currently in order to `Link Contract` you can't use predeployed contracts, but you can read the `Token Metadata URI` from the Collection to set your existing contracts' `setBaseMetadataURI`. The URI can be retrieved by accessing `Metadata URIs` purple button

![access metadata uris](img/collections/studio_collections_metadata_uris.png)

Then copy the `Token Metadata URI` from the modal and use the URI to write to a contract with the `setBaseMetadataURI` function, or, use to reference metadata directly in an application by appending a `<token_id>.json` to the URI to access the metadata

![copy metadata uris](img/collections/studio_collections_token_metadata_uri.png)