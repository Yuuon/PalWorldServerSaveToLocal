# 如何把幻兽帕鲁的私人服务器存档转移到个人电脑上以继续游玩
虽然现在谈这个有些早，但是当热度过去之后，肯定不少人会面对这个问题
当然，方法是有的，只是目前有些麻烦，如果有人喜欢写小工具的话可以考虑做个一键工具什么的
先说一点小理论知识：
其实多少要感谢0.1.2版本的退公会离线用户“坏档”BUG，如果不是这个BUG，恐怕解存档工具不会哪么快出来。
事实上，上面这个BUG，和服务器存档改单机的核心问题都是一个——即GUID保持一致，涉及到的GUID事实上有两个，一个是标识你存档名的GUID，另一个是代表你人在服务器里的Instance GUID，这两个保持一致即可（我想现行的个人转专用服务器存档教程也是类似的问题，只不过那边更麻烦一点）。
所以，要做的事情其实很简单，和你的服主要到服务器上的存档文件，然后，在 https://github.com/cheahjs/palworld-save-tools 工具的帮助下：
1. 把Level.sav文件转换成JSON并打开（小心，你需要足够的硬盘空间和一个能吃下可能达数G文本的文本编辑器——Visual code能打开，但是可能应该太长而不支撑全局替换）;
2. 然后，你需要找到你自己的存档GUID，全局搜索你的“昵称”，应该就可以找到（应该有两处，一处是基本玩家信息CharacterSaveParameterMap，另一处是公会信息，但是都有存档GUID）;
3. 找到你自己的存档GUID对应的文件，在存档文件夹的Players文件夹下，转换成JSON并打开，确认自己的Instance ID;
4. 首先确认自己存档GUID文件中SaveData:IndividualId:InstanceId的值，与Level.sav的JSON文件对照，应当有且仅有一处；如果没有，你需要在表worldSaveData:CharacterSaveParameterMap:key里，找到PlayerUId下对应自己存档GUID的结构，然后将其下方的InstanceId中的值改成与自己存档GUID的一致（随便改哪个，保持一样就行）;
5. 对Level.sav转换出的JSON文件进行全局替换——将自己的存档GUID全替换成00000000-0000-0000-0000-000000000001 ——单机模式下GUID一律是这个值;
6. 把自己的存档ID转化出的JSON文件中的自己的存档GUID也改成：00000000-0000-0000-0000-000000000001;
7. 现在，你应该有一个 **原本你的存档GUID已经全改成00000000-0000-0000-0000-000000000001** 的Level.sav.json，和一个 **原本你的存档GUID已经全改成00000000-0000-0000-0000-000000000001** 的存档GUID.sav.json文件，**且两个文件中代表你个人的Instance GUID一致**。把这两个文件用工具反向转化回.sav文件;
8. 最后把你的存档GUID的文件名改成00000000000000000000000000000001.sav即可;
9. 地图名称在LevelMeta.sav里，想改的也有样转JSON改完再转回去;
10. WorldOption.sav可以从其他单机存档里复制一个就行;

让我们最后再确认一下你的存档文件夹下应该有哪些东西：
X:\Users\[用户名]\AppData\Local\Pal\Saved\SaveGames\[SteamID]\[世界存档ID]下：
- 修改过的Level.sav文件
- 可以修改的LevelMeta.sav文件
- 不要动的LocalData.sav文件（你的图鉴进图，地图迷雾在这里，如果出问题了，去backup里找备份）
- 从别的存档里复制来的WorldOption.sav文件
- backup文件夹 —— 帕鲁自己的存档备份，如果有什么文件坏了可以尝试找这里的恢复
- Players文件夹 —— 用户存档在这里，其中应该有：
    - 00000000000000000000000000000001.sav 文件——你改好的自己的存档文件
    - 以及其他人的存档，你可以留着，也可以删了，不碍事

这样就完成了，运行帕鲁，单人模式下应该能看到追加的新世界，进入即可。
我已经成功了，所以这套方案是没问题的。如果有人失败的话，请检查是不是还有漏掉的GUID没改：请记住，核心就是保持各个文件中对应的GUID一致，另外如果你不放心操作前请备份文件，以防万一。


# How to transfer the private dedicated server save file of PalWorld to a single mode for continued gameplay
Although it may be a bit early to discuss this now, after the hype has passed, many people will definitely face this issue
Of course, there is a workaround. If someone can make a one-button script/tool would be nice.
First, a little theoretical knowledge:
In fact, we should be somewhat "thankful" for the "corrupt save" BUG of the 0.1.2 version, without this BUG, the save file tool might not have come out so quickly.
In fact, the above-mentioned BUG and the core issue of moving the server save file to single mode are the same - that is, keeping the GUID consistent. There are actually two GUIDs involved, one is the GUID that identifies your save data, and the other is the Instance GUID that represents you in the server, so what need to do is: make these two consistent (I think the current tutorial for converting personal save to dedicated server is a similar issue, but a bit more complicated over there).
So, the things to do are actually very simple, got the save files from your server host, and then, with the help of the tool at https://github.com/cheahjs/palworld-save-tools:
1. Convert the Level.sav file to JSON and open it (be careful, you need enough free disk space and a text editor that can handle possibly several GB of text - Visual code can open it, but it may be too long and not support Replace All function);
2. Then, you need to find your own save file GUID, search your "nickname" globally in Level.sav.json, you should be able to find it (there should be two places, one is CharacterSaveParameterMap, the other is guild information, either is fine);
3. Find the file corresponding to your own save file GUID, it should be in the Players folder, convert it to JSON and open it, and confirm your Instance ID;
4. Confirm the value of SaveData:IndividualId:InstanceId in your save file GUID file, compare it with the value in Level.sav.json, there should be one and only one; if not, you need to find the structure corresponding to your own save file GUID under table worldSaveData:CharacterSaveParameterMap:key, and then change the value of InstanceId below PlayerUId corresponding to your own save file GUID to be consistent with your own save file GUID (change whichever, just keep it the same);
5. Do a Replace All(if possible, or you can go all manually) on the Level.sav.json - replace all occurrences of your save file GUID with 00000000-0000-0000-0000-000000000001 -- in single mode, the GUID is always this value;
6. Change your save file GUID in the JSON file converted to: 00000000-0000-0000-0000-000000000001;
7. Now, you should have a Level.sav.json where **originally your save file GUID has been completely changed to 00000000-0000-0000-0000-000000000001**, and a save file GUID.sav.json where **originally your save file GUID has been completely changed to 00000000-0000-0000-0000-000000000001**, **and the Instance GUID representing you in both files is consistent**. Use the tool to convert these two files back to .sav files;
8. Finally, change the file name of your save file GUID to 00000000000000000000000000000001.sav;
9. The map name is in LevelMeta.sav, if you want to change it, convert it to JSON, make the changes, and then convert it back;
10. You can just copy WorldOption.sav from another single mode save file;

Let's confirm once again what should be in your save file folder:
X:\Users\[username]\AppData\Local\Pal\Saved\SaveGames\[SteamID]\[world ID]:
- Modified Level.sav file
- Optional Modified LevelMeta.sav file
- Do not touch LocalData.sav file (your collection progress, map view is here, if there is a problem, look for backups in the backup folder)
- WorldOption.sav copied from another save file
- backup folder - PalWorld's own save file backup, if any files are corrupted, you can try to find a recovery here
- Players folder - user save files are here, among which there should be:
    - 00000000000000000000000000000001.sav file - your modified save file
    - and other people's save files, you can keep them or delete them, it doesn't matter

That's it, once done, run PalWorld, in single mode you should see the newly added world, just enter and play.
I have succeeded, so this solution is reliable. If someone fails, please check if there are any missed GUIDs to change: remember, the key is to keep the corresponding GUIDs consistent in each file, and if you are not confident before operating, please back up the files, just in case.