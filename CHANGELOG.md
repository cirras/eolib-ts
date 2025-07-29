# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.0.1] - 2025-07-29

### Fixed

- Fix inaccurate deserialization of `WelcomeReplyServerPacket` where non-chunked portions of the
  data structure were being treated as if they were chunked.

## [2.0.0] - 2025-06-28

### Added

- `SpellReplyServerPacket` packet class.
- `SkillStatRequirements` class.
- `PlayerEffect` class.
- `TileEffect` class.
- `EffectPlayerServerPacket.effects` field.
- `EffectAgreeServerPacket.effects` field.
- `AdminInteractTellServerPacket.goldBank` field.

### Changed

- Rename `QuestReportServerPacket.npcId` field to `npcIndex`.
- Make `CastReplyServerPacket.casterTp` field optional.
- Make `CastSpecServerPacket.casterTp` field optional.
- Make `CastAcceptServerPacket.casterTp` field optional.
- Make `CastAcceptServerPacket.experience` field optional.
- Make `CastAcceptServerPacket.levelUp` field optional.
- Make `NpcAcceptServerPacket.experience` field optional.
- Make `NpcAcceptServerPacket.levelUp` field optional.
- Change `TradeItemData` to represent a single player's trade items instead of both trade partners.
- Change `TradeReplyServerPacket.tradeData` field type from `TradeItemData` to `TradeItemData[]`.
- Change `TradeAdminServerPacket.tradeData` field type from `TradeItemData` to `TradeItemData[]`.
- Change `TradeUseServerPacket.tradeData` field type from `TradeItemData` to `TradeItemData[]`.

### Removed

- `EffectPlayerServerPacket.playerId` field.
- `EffectPlayerServerPacket.effectId` field.
- `EffectAgreeServerPacket.coords` field.
- `EffectAgreeServerPacket.effectId` field.

### Fixed

- Fix incorrect (de)serialization of `EffectPlayerServerPacket` due to only the first effect in the
  array being recognized.
- Fix incorrect (de)serialization of `EffectAgreeServerPacket` due to only the first effect in the
  array being recognized.
- Fix inaccurate serialization of `QuestAcceptClientPacket` where the char value 0 should be written
  for `DialogReply.Ok`.
- Fix inaccurate serialization of `AccountReplyServerPacket` where the string value "OK" should be
  written for `AccountReply.Changed`, but "NO" was being written instead.
- Fix inaccurate serialization of `AdminInteractTellServerPacket` where the `goldBank` field was
  missing.
- Fix inaccurate serialization of `RecoverPlayerServerPacket` where a trailing 0 short value was
  missing.
- Fix inaccurate serialization of `ShopOpenServerPacket` where a trailing break byte was erroneously
  being written.
- Fix inaccurate serialization of `DoorOpenServerPacket` where a trailing 0 char value was
  erroneously being written.
- Change incorrect `CharacterStatsInfoLookup.secondaryStats` field type from
  `CharacterSecondaryStats` to `CharacterSecondaryStatsInfoLookup`.
- Change incorrect `SkillLearn.statRequirements` field type from `CharacterBaseStats` to
  `SkillStatRequirements`.

## [1.1.1] - 2025-06-28

### Fixed

- Errors when consuming the library as an ESM. ("ReferenceError: exports is not defined")

## [1.1.0] - 2025-06-28

### Added

- Support for server pub files:
  - `DropRecord` class.
  - `DropNpcRecord` class.
  - `DropFile` class.
  - `InnQuestionRecord` class.
  - `InnRecord` class.
  - `InnFile` class.
  - `SkillMasterSkillRecord` class.
  - `SkillMasterRecord` class.
  - `SkillMasterFile` class.
  - `ShopTradeRecord` class.
  - `ShopCraftIngredientRecord` class.
  - `ShopCraftRecord` class.
  - `ShopRecord` class.
  - `ShopFile` class.
  - `TalkMessageRecord` class.
  - `TalkRecord` class.
  - `TalkFile` class.
- `GuildTakeClientPacket.guildTag` field.

### Fixed

- Fix incorrect (de)serialization of `NpcAgreeServerPacket` due to the `npcs` array's length being
  treated as a `short` instead of `char`.
- Fix incorrect (de)serialization of `GuildTakeClientPacket` due to missing `guildTag` field.
- Fix incorrect (de)serialization of `AvatarAdminServerPacket` due to incorrect ordering of the
  `casterDirection` and `damage` fields.
- Fix inaccurate (de)serialization of `JukeboxMsgClientPacket` due to the packet being treated as a
  chunked data structure.

## [1.0.2] - 2025-06-09

### Fixed

- Import resolution errors under node (notably `ERR_UNSUPPORTED_DIR_IMPORT` and `ERR_REQUIRE_ESM`).
- Incorrect (de)serialization of some data structures containing arrays with trailing delimiters.
- String sanitization within chunked sections of protocol data structures.
  - Generated code now sets `EoWriter.stringSanitizationMode` during serialization.
  - For more information, see
    [Chunked Reading: Sanitization](https://github.com/Cirras/eo-protocol/blob/master/docs/chunks.md#sanitization).

## [1.0.1] - 2023-12-18

### Changed

- Remove trailing break from `ArenaSpecServerPacket`.
- Remove trailing break from `ArenaAcceptServerPacket`.

## [1.0.0] - 2023-11-07

### Added

- `BankAddClientPacket.sessionId` field.
- `BankTakeClientPacket.sessionId` field.

## [1.0.0-rc.7] - 2023-08-04

### Added

- `EoReader.slice` method.

### Removed

- `TradeRequestServerPacket.unk1` field.
- `TradeCloseClientPacket.unk1` field.
- `PlayersList.onlineCount` field.
- `PlayersListFriends.onlineCount` field.

### Fixed

- Fix incorrect (de)serialization of `NpcRangeRequestClientPacket`.
- Fix bug where `EoReader.remaining` could return a negative number.

## [1.0.0-rc.6] - 2023-06-21

### Changed

- Rename `SkillLearn.levelReq` field to `levelRequirement`.
- Rename `SkillLearn.classReq` field to `classRequirement`.
- Rename `SkillLearn.skillReq` field to `skillRequirement`.
- Rename `CitizenRequestClientPacket.behaviourId` field to `behaviorId`.
- Rename `CitizenAcceptClientPacket.behaviourId` field to `behaviorId`.
- Rename `CitizenReplyClientPacket.behaviourId` field to `behaviorId`.
- Rename `CitizenRemoveClientPacket.behaviourId` field to `behaviorId`.
- Rename `CitizenOpenServerPacket.behaviourId` field to `behaviorId`.
- Rename `QuestDialogServerPacket.behaviourId` field to `behaviorId`.
- Rename `EnfRecord.behaviourId` field to `behaviorId`.

### Fixed

- Import resolution failures when consuming the library as an ESM.

## [1.0.0-rc.5] - 2023-05-13

### Added

- `WarpEffect.None` enum value.

### Changed

- Change `MapTileSpecRowTile.tileSpec` field type from `char` to `MapTileSpec`.

### Fixed

- Change incorrect `ChestReplyServerPacket.remainingAmount` field type from `short` to `int`.

## [1.0.0-rc.4] - 2023-05-02

### Added

- Support for new `blob` type, which maps to `Uint8Array`.

### Changed

- Rename `ItemType.Money` to `Currency`.
- Rename `ItemType.Beer` to `Alcohol`.
- Change `EsfRecord.element` field type from `char` to `Element`.
- Improve docs on `EifRecord.spec*` fields.
- Change `EmfFile.content` field type from array of `byte` to `blob`.
- Change `PubFile.content` field type from array of `byte` to `blob`.

### Fixed

- Change incorrect `WalkCloseServerPacket` dummy value from `f` to `S`.
- Change incorrect `WalkOpenServerPacket` dummy value from `u` to `S`.
- Change incorrect `ByteCoords.x` field type from `short` to `byte`.
- Change incorrect `ByteCoords.y` field type from `short` to `byte`.

## [1.0.0-rc.3] - 2023-04-08

### Added

- Sanitize `0xFF` bytes in strings when writing chunked data structures.

### Changed

- Rename `AdminLevel.Guide` enum value to `Spy`.
- Rename `AdminLevel.Guardian` enum value to `LightGuide`.
- Rename `AdminLevel.Gm` enum value to `Guardian`.
- Rename `AdminLevel.Hgm` enum value to `GameMaster`.
- Rename `AdminLevel.Reserved5` enum value to `HighGameMaster`.
- Rename `ServerSettings.lightGuideFloodRate` field to `spyAndLightGuideFloodRate`.
- Rename `ServerSettings.gameMasterAndHighGameMasterFloodRate` field to `gameMasterFloodRate`.
- Rename `ServerSettings.reserved5FloodRate` field to `highGameMasterFloodRate`.
- Add missing `PaperdollRemoveServerPacket.itemId` field.
- Add missing `PaperdollRemoveServerPacket.subLoc` field.
- Add missing `PaperdollAgreeServerPacket.itemId` field.
- Add missing `PaperdollAgreeServerPacket.remainingAmount` field.
- Add missing `PaperdollAgreeServerPacket.subLoc` field.

### Fixed

- Change incorrect `LockerGetServerPacket.takenItem` field type from `Item` to `ThreeItem`.

## [1.0.0-rc.2] - 2023-02-16

### Added

- `Element` enum.
- `PacketFamily.Error` enum value.
- `PacketAction.Error` enum value.
- `PacketAction.Net243` enum value.
- `PacketAction.Net244` enum value.
- `TalkPlayerClientPacket` packet class.
- `TalkUseClientPacket` packet class.
- `AttackErrorServerPacket` packet class.
- `SpellErrorServerPacket` packet class.
- `WarpPlayerServerPacket` packet class.
- `WarpCreateServerPacket` packet class.
- `WelcomePingServerPacket` packet class.
- `WelcomePongServerPacket` packet class.
- `WelcomeNet242ServerPacket` packet class.
- `WelcomeNet243ServerPacket` packet class.
- `WelcomeNet244ServerPacket` packet class.
- `PlayersListServerPacket` packet class.
- `PlayersReplyServerPacket` packet class.
- `MapFile` class.
- `PubFile` class.
- `PlayersList` class.
- `PlayersListFriends` class.

### Changed

- Rename `ItemType.Spell` enum value to `Reserved5`.
- Rename `PacketAction.Net3` enum value to `Net242`.
- Rename `InitReply.Players` enum value to `PlayersList`.
- Rename `InitReply.FriendsListPlayers` enum value to `PlayersListFriends`.
- Change `EifRecord.element` field type from `char` to `Element`.
- Change `EnfRecord.element` field type from `short` to `Element`.
- Change `EnfRecord.elementWeakness` field type from `short` to `Element`.
- Change incorrect `QuestRequirementIcon` underlying type from `char` to `short`.
- Roll `InitInitServerPacket.ReplyCodeDataWarpMap` fields into new `mapFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataFileEmf` fields into new `mapFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataFileEif` fields into new `pubFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataFileEnf` fields into new `pubFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataFileEsf` fields into new `pubFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataFileEcf` fields into new `pubFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataMapMutation` fields into new `mapFile` field.
- Roll `InitInitServerPacket.ReplyCodeDataPlayersList` fields into new `playersList` field.
- Roll `InitInitServerPacket.ReplyCodeDataPlayersListFriends` fields into new `playersList` field.

## [1.0.0-rc.1] - 2023-02-09

### Added

- Support for EO data structures:
  - Client packets
  - Server packets
  - Endless Map Files (EMF)
  - Endless Item Files (EIF)
  - Endless NPC Files (ENF)
  - Endless Spell Files (ESF)
  - Endless Class Files (ECF)
- Utilities:
  - Data reader
  - Data writer
  - Number encoding
  - String encoding
  - Data encryption
  - Packet sequencer

[Unreleased]: https://github.com/cirras/eolib-ts/compare/v2.0.1...HEAD
[2.0.1]: https://github.com/cirras/eolib-ts/compare/v2.0.0...v2.0.1
[2.0.0]: https://github.com/cirras/eolib-ts/compare/v1.1.1...v2.0.0
[1.1.1]: https://github.com/cirras/eolib-ts/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/cirras/eolib-ts/compare/v1.0.2...v1.1.0
[1.0.2]: https://github.com/cirras/eolib-ts/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/cirras/eolib-ts/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.7...v1.0.0
[1.0.0-rc.7]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.6...v1.0.0-rc.7
[1.0.0-rc.6]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.5...v1.0.0-rc.6
[1.0.0-rc.5]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.4...v1.0.0-rc.5
[1.0.0-rc.4]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.3...v1.0.0-rc.4
[1.0.0-rc.3]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.2...v1.0.0-rc.3
[1.0.0-rc.2]: https://github.com/cirras/eolib-ts/compare/v1.0.0-rc.1...v1.0.0-rc.2
[1.0.0-rc.1]: https://github.com/cirras/eolib-ts/releases/tag/v1.0.0-rc.1
