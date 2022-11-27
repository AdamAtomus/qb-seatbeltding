# qb-seatbeltding
A basic block of code that plays a seatbelt noise until you put the seatbelt on, it will stop after 4 dings for 25 seconds
## How to install

1. Add nobelt.ogg to interact-sound/client/html/sounds (Commonly located in /resources/[standalone]/interact-sound/client/html/sounds)
2. Add the code below to qb-smallresources/client/seatbelt.lua (Commonly located in /resources/[qb]/qb-smallresources/client/seatbelt.lua)



```
timesplayed = 0
CreateThread(function()
    while true do
        if IsPedInAnyVehicle(PlayerPedId(), false) then
            local class = GetVehicleClass(GetVehiclePedIsUsing(PlayerPedId()))
            if class ~= 8 and class ~= 13 and class ~= 14 then
                if not seatbeltOn and not harnessOn then
                    if timesplayed > 4 then -- It will play 4 times before stopping for 25 seconds
                        timesplayed = 0
                        Wait(25000)
                    else
                        timesplayed = timesplayed + 1
                        TriggerServerEvent("InteractSound_SV:PlayOnSource", "nobelt", 0.25)
                        Wait(1500) -- how long until it plays the ogg
                    end
                end
            end
        end
        Wait(1500)
    end
end)
```
Here is a version that constantly plays until you put the belt on
```
CreateThread(function()
    while true do
        if IsPedInAnyVehicle(PlayerPedId(), false) then
            local class = GetVehicleClass(GetVehiclePedIsUsing(PlayerPedId()))
            if class ~= 8 and class ~= 13 and class ~= 14 then
                if not seatbeltOn and not harnessOn then
                    TriggerServerEvent("InteractSound_SV:PlayOnSource", "nobelt", 0.25)
                end
            end
        end
        Wait(1500)
    end
end)
```

## Adding a Custom sounds

You can simply convert any audio file to a .ogg but you might have to change the length
