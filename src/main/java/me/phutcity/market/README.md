# PhutCityMarket 0.1.0 (source)

Plugin skeleton for PHUT CITY's native Minecraft Shelf block. Designed for Paper 26.3 and Geyser/Floodgate cross-play.

## Current build scope
- `/marketadmin` opens the manager for the Shelf block the admin is looking at (within 6 blocks).
- Right-clicking a native `*_SHELF` block as OP or `phutcity.market.admin` opens the same manager.
- A shelf has exactly three product positions.
- Shift-click an item from the player's inventory to add it to the first free product position.
- Put an item on the cursor and click a product position to replace/set that product.
- Click a product position with an empty cursor to enter its price in chat; type `huy` to cancel.
- Shift + right-click a product position to remove it.
- Press SAVE to persist the shelf. Product data is stored in `plugins/PhutCityMarket/shelves.yml`.
- ItemDisplay entities render the configured products in front of the real Shelf block. They are tagged and removed/recreated when that shelf is saved; breaking the shelf removes its data and display entities.
- Non-admin players cannot manipulate the Shelf block directly, preventing free removal of the display stock.

## Important limitations of 0.1.0
This is the **admin shelf setup module only**. Customer shopping carts, checkout NPC, cash/bank charging, stock decrementing, receipts, and exit-gate validation are not implemented yet. They require the PHUT CITY economy API or a clearly specified economy bridge. This version does not pretend to charge players without that integration.

The shelf's three visible product positions are rendered with ItemDisplay entities managed by this plugin. They are not the vanilla shelf's internal item storage. This avoids depending on Minecraft internals; Paper's public `Shelf` block-data interface exposes facing/power/waterlogging/side-chain properties rather than a Bukkit inventory.

## Build
Requires JDK 25 and Gradle 9.x (or compatible Gradle with Java 25 toolchain).

```bash
gradle build
```

Output: `build/libs/PhutCityMarket-0.1.0.jar`

## Install
1. Stop the Paper server.
2. Put the built JAR in `plugins/`.
3. Start the server.
4. In-game, look directly at a native Shelf block and run `/marketadmin`, or right-click it as OP.
5. Add products and set prices, then press SAVE.

Permission: `phutcity.market.admin` (default: OP).

## Build without a PC (GitHub Actions option)
The project includes `.github/workflows/build.yml`. Upload the project contents to a GitHub repository, open **Actions**, choose **Build PhutCityMarket**, and run the workflow. Download the `PhutCityMarket-0.1.0` artifact; it contains the JAR produced by Gradle. Do not install the source ZIP itself on the Minecraft server.
