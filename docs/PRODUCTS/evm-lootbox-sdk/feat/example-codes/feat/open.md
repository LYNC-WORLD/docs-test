---
sidebar_label: 'Example code for opening a new lootbox'
id: evm-lootbox-sdk-example-codes-open
custom_edit_url: null
---

# Example code for opening a new lootbox

## Example:
```typescript
import { ChainIdentifier, LootBoxError, LyncLootBox } from "@lyncworld/lootbox-evm-sdk";

const lootbox = new LyncLootBox();
const provider = new ethers.providers.Web3Provider(window.ethereum);

const lootboxId = "0x..." // a valid lootbox id created using `createLootBox` method

lootbox
	.initialize(ChainIdentifier.BASE_SEPOLIA, provider, lootboxId)
	.then((response) => console.log(response))
	.catch((err) => console.error("Error in initializing lootbox: ", err));

async function openLootbox() {
    try {
      const isEmpty = await lootbox.isEmpty();

      if (isEmpty) return;

      const signer = provider.getSigner();
      const responseData = await lootbox.openLootBox(signer);
      console.log("Transaction response: ", responseData);
    } catch (err: unknown) {
      console.error("Error in handleLootBoxOpen: ", err);

      if (err instanceof LootBoxError || err instanceof Error) {
        console.error(err.message);
      } else {
        console.error("Something went wrong! Please refresh and try again.");
      }
    }
  }
```
