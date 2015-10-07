##SQL Useful Queries:

###Default template to change an value of an Table_Row of an ID OR Name

    UPDATE `Database_table` SET `Table_Row` = Value  WHERE `entry` LIKE 'ID_Here';
    UPDATE `Database_table` SET `Table_Row` = Value  WHERE `Name` LIKE '%Name_Here%';

    example:
    UPDATE `Item_template` SET dmg_min1 = 1234 WHERE `entry` LIKE 'ID_Here';
    UPDATE `Item_template` SET dmg_min1 = 1234 WHERE `Name` LIKE '%Name_Here%';

###Play sound on quest accept

    SET @Sound :=1234;  -- Replace with desired sound ID you wish you play.
    SET @Start :=5555; -- Replace with Unique ID for end Script, set this to whatever you want.
    SET @Quest :=25; -- Replace with Quest ID wished to link sound to.
    INSERT INTO `quest_start_scripts` VALUES (@Start, 1, 16, @Sound, 1, 0, 0, 0, 0, 0);
    UPDATE `quest_template` SET startscript=@Start WHERE id=@Quest;    

###Remove the "Level 80" Mail

    DELETE FROM `achievement_reward` WHERE `entry` = "13";

###Remove all spellcosts in trainers and remove all itemcosts in vendors.

    UPDATE `npc_trainer` SET `spellcost` = 0;
    UPDATE `item_template` SET `buycost` = 0;

###Disable a spell in a certain zone

    SET @entry :=1234;  -- Replace with the Spell ID.
    SET @params_1 :=5555; -- Replace with the Zone ID.
    SET @comment :=Spell Disable; -- Replace with any comment.
    INSERT INTO `disables` VALUES (3, @entry, 49, 0, @params_1, @comment);

###Set starting zone for all races/classes

    SET @map :=1234;  -- Replace with the Map ID.
    SET @zone :=1234; -- Replace with the Zone ID.
    SET @position_x :=1234; -- Replace with Position_x.
    SET @position_y :=1234;  -- Replace with the Position_y.
    SET @position_z :=1234; -- Replace with the Position_z.
    SET @orientation :=1234; -- Replace with Orientation.
    UPDATE `playercreateinfo` SET map=@map AND zone=@zone AND position_x=@position_x AND position_y=@position_y AND     position_z=@position_z AND orientation=@orientation WHERE race>=1 AND race<=11;

###Set Starting zone of Horde Races

    SET
    @MAP := 'MAP',
    @ZONE := 'ZONE',
    @X := 'X-Cordinate',
    @Y := 'Y-Cordinate',
    @Z := 'Z-Cordinate',
    @O := 'Orientation';

    UPDATE playercreateinfo SET map=@MAP, zone=@ZONE, position_X=@X, position_Y=@Y, position_Z=@Z, orientation=@O WHERE race IN(2, 5, 6, 8, 10);

###Set Starting zone of Alliance Races

    SET
    @MAP := 'MAP',
    @ZONE := 'ZONE',
    @X := 'X-Cordinate',
    @Y := 'Y-Cordinate',
    @Z := 'Z-Cordinate',
    @O := 'Orientation';

    UPDATE playercreateinfo SET map=@MAP, zone=@ZONE, position_X=@X, position_Y=@Y, position_Z=@Z, orientation=@O WHERE race IN(1, 3, 4, 7, 11);

###Set the required level on an item

    UPDATE `Item_template` SET requiredLevel = required level WHERE `Name` LIKE '%Name on item here%';

###Set minimal and maximal damage on an item

    UPDATE `Item_template` SET dmg_min1 = Min DMG WHERE `Name` LIKE '%Name on item here%';
    UPDATE `Item_template` SET dmg_max1 = Max DMG WHERE `Name` LIKE '%Name on item here%';

###Set Allowable Class to an item

    UPDATE `Item_template` SET AllowableClass = Class id here WHERE `entry` LIKE '%Entry id on item  here%';

###Change a certain part of an name of an item

CONCAT merges strings together
SUBSTRING gets a part of a string, in this case the name of the item (example: the Claymore part)
LENGTH calculates the length of the string. I used it there so you can change the string to take away from the beginning of the name.
So, "Relentless " is erased and "Starter " is placed in it's place for all items with name like "Relentless Gladiator's "..

    UPDATE item_template SET name = CONCAT("Starter ", SUBSTRING(name, LENGTH("Relentless ")+1)) WHERE name like "Relentless Gladiator's %";

###This sql will update your item sets stats by specific set name.
So if you want all wrathful items updated 15% stats more this is how, but if you want some other Set just replace wrathful.
and if u want more % just change number 1.15 if 25% = 1.25 etc

    UPDATE `Item_template` SET stat_value1 = (stat_value1 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value2 = (stat_value2 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value3 = (stat_value3 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value4 = (stat_value4 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value5 = (stat_value5 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value6 = (stat_value6 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value7 = (stat_value7 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value8 = (stat_value8 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value9 = (stat_value9 * 1.15) WHERE `Name` LIKE '%Wrathful%';
    UPDATE `Item_template` SET stat_value10 = (stat_value10 * 1.15) WHERE `Name` LIKE '%Wrathful%';

###This sql will update your item stats by specific ID.
So if you want all items of Id (ID) updated 15% stats more this is how, but if you want some other Set just replace wrathful.
and if u want more % just change number 1.15 if 25% = 1.25 etc

    UPDATE `Item_template` SET stat_value1 = (stat_value1 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value2 = (stat_value2 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value3 = (stat_value3 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value4 = (stat_value4 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value5 = (stat_value5 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value6 = (stat_value6 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value7 = (stat_value7 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value8 = (stat_value8 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value9 = (stat_value9 * 1.15) WHERE entry LIKE 'ID';
    UPDATE `Item_template` SET stat_value10 = (stat_value10 * 1.15) WHERE entry LIKE 'ID';

###Change all itemLevel with Name Or ID

    UPDATE `Item_template` SET itemLevel = ItemLevelHere WHERE name LIKE '%%';
    UPDATE `Item_template` SET itemLevel = ItemLevelHere WHERE entry LIKE 'ID';

###Delete Itemset from Name or ID

    UPDATE `Item_template` SET itemSet = 0 WHERE name LIKE '%%';
    UPDATE `Item_template` SET itemSet = 0 WHERE entry LIKE 'ID';

###Delete Itemset from Name or ID

    UPDATE `Item_template` SET itemSet = 0 WHERE name LIKE '%%';
    UPDATE `Item_template` SET itemSet = 0 WHERE entry LIKE 'ID';

###Delete Itemset from Name or ID

    UPDATE `Item_template` SET itemSet = 0 WHERE name LIKE '%%';
    UPDATE `Item_template` SET itemSet = 0 WHERE entry LIKE 'ID';

###Copy an existing DisplayID

    SET @myItem = '96000'; /* entry of your item */
    SET @copyItem = 'Hearthstone'; /* name of item to copy */

    SET @myValue = (SELECT displayid FROM item_template WHERE NAME LIKE @copyItem);
    UPDATE item_template
    SET displayid=@myValue
    WHERE entry=@myItem;

###Make an simple NPC

    SET @Entry :=50003;
    SET @ModelID :=27436;
    SET @Name :='Name Here';
    SET @Subname :='Subname Here';
    SET @NPCFLAG :=2; -- 1 is gossip / scripted npc's, 4224 is vendor
    DELETE FROM `creature_template` WHERE `entry`=@Entry;
    INSERT INTO `creature_template` (`entry`, `difficulty_entry_1`, `difficulty_entry_2`, `difficulty_entry_3`, `KillCredit1`, `KillCredit2`, `modelid1`, `modelid2`, `modelid3`, `modelid4`, `name`, `subname`, `IconName`, `gossip_menu_id`, `minlevel`, `maxlevel`, `exp`, `faction_A`, `faction_H`, `npcflag`, `speed_walk`, `speed_run`, `scale`, `rank`, `mindmg`, `maxdmg`, `dmgschool`, `attackpower`, `dmg_multiplier`, `baseattacktime`, `rangeattacktime`, `unit_class`, `unit_flags`, `unit_flags2`, `dynamicflags`, `family`, `trainer_type`, `trainer_spell`, `trainer_class`, `trainer_race`, `minrangedmg`, `maxrangedmg`, `rangedattackpower`, `type`, `type_flags`, `lootid`, `pickpocketloot`, `skinloot`, `resistance1`, `resistance2`, `resistance3`, `resistance4`, `resistance5`, `resistance6`, `spell1`, `spell2`, `spell3`, `spell4`, `spell5`, `spell6`, `spell7`, `spell8`, `PetSpellDataId`, `VehicleId`, `mingold`, `maxgold`, `AIName`, `MovementType`, `InhabitType`, `HoverHeight`, `Health_mod`, `Mana_mod`, `Armor_mod`, `RacialLeader`, `questItem1`, `questItem2`, `questItem3`, `questItem4`, `questItem5`, `questItem6`, `movementId`, `RegenHealth`, `mechanic_immune_mask`, `flags_extra`, `ScriptName`, `WDBVerified`) VALUES
    (@Entry, 0, 0, 0, 0, 0, @ModelID, 0, 0, 0, @Name, @Subname, '', 0, 80, 80, 2, 35, 35, @NPCFLAG, 1, 1.14286, 1, 3, 10, 10, 0, 0, 1, 1000, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, '', 0, 3, 1, 10000, 0, 100, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, '', 1);

###Create teleport Portals (Object)

    @GOB_Name := ID_Here,
    @GOB_Name := Name_Here,
    @GOB_Display := DisplayID_Here,
    @Event_scriptID := 33333,
    @MAP := 0,
    @X := -1825.442139,
    @Y := -4222.890625,
    @Z := 3.861495,
    @O := 4.181533;
 
    INSERT INTO `gameobject_template` (`entry`, `type`, `displayId`, `name`, `size`, `data2`) VALUES (@GOB_Entry, 10, @GOB_Display, @GOB_Name, 1, @Event_scriptID);
    REPLACE INTO `event_scripts` (`id`, `command`, `datalong`, `x`, `y`, `z`, `o`) VALUES (@Event_scriptID, 6, @MAP, @X, @Y, @Z, @O);

###Updates the broadcast with the desired broadcast and color

    SET @Text := '|cffffff00[|c00077766Broadcast_Here|cffffff00]: |cFFF222FF%s|r';

    UPDATE trinity_string SET content_default=@Text WHERE entry=11000 LIMIT 1;