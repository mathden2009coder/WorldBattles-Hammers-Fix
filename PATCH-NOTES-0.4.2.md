# 0.4.2 patch notes

Patched `WorldBattlesHammers.tick` to replace the `ServerPlayerGameMode.destroyBlock(BlockPos)` call for neighboring 3x3 blocks with the level-level destroy API (`Level.destroyBlock(BlockPos, boolean, Entity)`). This avoids invoking the player game-mode single-target destroy path for a neighboring position, which is the suspected source of `Mismatch in destroy block pos` warnings.

The original recipes, textures, item classes, and metadata are preserved in the patched JAR. This bytecode patch has been structurally inspected with `javap` and the ZIP archive integrity checker. It has not yet been tested inside a live Forge 1.20.1 server, so treat it as a test build until the in-game checks pass.