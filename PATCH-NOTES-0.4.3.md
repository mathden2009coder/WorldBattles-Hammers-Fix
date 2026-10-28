# WorldBattles Hammers 0.4.3 — test build

This patch is based on the user's original WorldBattles Hammers JAR and the 3x3 processing approach observed in `hammers-2.1.5-1.20.1-forge.jar`.

Changes to the compiled class:
- Replace the queued-neighbor call to `ServerPlayerGameMode.destroyBlock(BlockPos)` (the single-position game-mode path) with a dedicated drop-aware helper.
- Pass the actual main-hand hammer to `Block.dropResources`, so Fortune-aware loot logic can see the held tool.
- Remove the block without a second drop pass and calculate block XP using the held tool's Fortune/Silk Touch enchantment levels.
- Keep original item registration, names, recipes, textures, and other archive resources unchanged.

Validation: ZIP integrity checked and bytecode inspected. This is not a Forge runtime test; test on a backup world/server before using it live. Because this helper bypasses the player game-mode break call, protection/claim integrations and exact durability behavior still need in-game verification.