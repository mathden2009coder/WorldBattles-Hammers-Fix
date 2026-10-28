# WorldBattles Hammers Fix

Forge 1.20.1 patch project for the WorldBattles hammers mod.

Goals:
- Remove `Mismatch in destroy block pos` warnings by fixing the 3x3 block-destruction path.
- Ensure all eligible blocks in the 3x3 area are processed with Efficiency V.
- Preserve Fortune drops, miner-profession XP, protection checks, tool durability, recipes, and textures.

The original compiled JAR is used as the baseline because Java source files were not provided. A release is only considered ready after a successful build and in-game verification.