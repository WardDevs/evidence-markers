# evidence-markers
this is an evidence marker for qbcore for police to use it credits to the original [author of the prop](https://www.gta5-mods.com/misc/plastic-evidence-markers)



## you need to do this things


## First add this to your qb-policejob/config.lua under Config.Objects
```lua
["evidence"] = {model = `ril1`, freeze = true},
```


## Second (this step is optional) add this to your qb-policejob/client/object.lua:137 (use this if you want to use it with radialmenu)
```lua
RegisterNetEvent('police:client:SpawnEvidenceMarker', function()
    QBCore.Functions.Progressbar("spawn_object", Lang:t("progressbar.place_object"), 2500, false, true, {
        disableMovement = true,
        disableCarMovement = true,
        disableMouse = false,
        disableCombat = true,
    }, {
        animDict = "anim@narcotics@trash",
        anim = "drop_front",
        flags = 16,
    }, {}, {}, function() -- Done
        StopAnimTask(PlayerPedId(), "anim@narcotics@trash", "drop_front", 1.0)
        TriggerServerEvent("police:server:spawnObject", "evidence")
    end, function() -- Cancel
        StopAnimTask(PlayerPedId(), "anim@narcotics@trash", "drop_front", 1.0)
        QBCore.Functions.Notify(Lang:t("error.canceled"), "error")
    end)
end)
```


## Then (this step is also optional) add this to your qb-radialmenu/config.lua (use this if you want to use it with radialmenu)
```lua
{
    id = 'evidencemarker',
    title = 'Evidence Marker',
    icon = 'caret-up',
    type = 'client',
    event = 'police:client:SpawnEvidenceMarker',
    shouldClose = false
},
```
### Done!
