# QbusToEsx Qbus Scriptleri ESX e Çevirme.
--------------------------------------------------------------------------------------------------
 ```lua
QBCore = nil 

Citizen.CreateThread(function()
	while QBCore == nil do
		TriggerEvent('QBCore:GetObject', function(obj) QBCore = obj end)
		Citizen.Wait(31)
	end
end)
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
ESX = nil

Citizen.CreateThread(function()
  while ESX == nil do
    TriggerEvent('esx:getSharedObject', function(obj) ESX = obj end)
    Citizen.Wait(31)
  end
end)
```
--------------------------------------------------------------------------------------------------
```lua
RegisterNetEvent('QBCore:Client:OnPlayerLoaded')
AddEventHandler('QBCore:Client:OnPlayerLoaded', 
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
RegisterNetEvent('esx:playerLoaded')
AddEventHandler('esx:playerLoaded',
```
--------------------------------------------------------------------------------------------------
```lua
RegisterNetEvent('QBCore:Client:OnJobUptade')
AddEventHandler('QBCore:Client:OnJobUptade', 
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
RegisterNetEvent('esx:setJob')
AddEventHandler('esx:setJob',
```
--------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.DrawText3D(1, 1, 1, 'Örnek')
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
DrawText3D(1, 1, 1, 'Örnek') -- (aşağısına function açmanız gerekmektedir.)
```
--------------------------------------------------------------------------------------------------
```lua
QBCore.UI.Menu.Open
QBCore.UI.Menu.CloseAll() -- (menu default scripti kurmanız gerekmektedir.)
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
ESX.UI.Menu.Open
ESX.UI.Menu.CloseAll()
```
--------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.Notify("Araç kitlendi.", "error")
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
TriggerEvent('Notification',"Örnek.")
```
--------------------------------------------------------------------------------------------------
```lua
xPlayer.Functions.GetItemByName 
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
xPlayer.getInventoryItem
```
--------------------------------------------------------------------------------------------------
```lua
xPlayer.Functions.RemoveItem 
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
xPlayer.removeInventoryItem 
```
--------------------------------------------------------------------------------------------------
```lua
xPlayer.Functions.AddItem
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
xPlayer.addInventoryItem
```
--------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.GetPlayer(src)
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
ESX.GetPlayerFromId(src)
```
--------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.SpawnVehicle()
QBCore.Functions.GetVehicleProperties()
QBCore.Functions.GetClosestVehicle()
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
ESX.Game.SpawnVehicle()
ESX.Game.GetVehicleProperties()
ESX.Game.GetClosestVehicle()
```
--(Eğer ESX.Game olan neredeyse her şey QBCore.Functions olarak aynı şekildedir.)
------------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.GetPlayerData()
```
#ÜSTEKİ QBUSCORE

#ALTAKİ ESX
```lua
ESX.GetPlayerData()
```
---------------------------------------------------------------------------------------------------
QBCore.Functions.CreateUseableItem()

ESX.RegisterUsableItem()
--------------------------------------------------------------------------------------------------
QBCore.Functions.CreateCallback()

ESX.RegisterServerCallback()
-----------------------------------------------------------------------------------------------------------
QBCore.Functions.TriggerCallback()

ESX.TriggerServerCallback()
-----------------------------------------------------------------------------------------------------------
**-- qb'de cid esx'de identifier kullanılıyor olayı çözmeniz için ufak bir kod bloğu bıraktık.**
```lua
QBCore.Functions.CreateCallback('system:fetchStatus', function(source, cb)
    local Player = QBCore.Functions.GetPlayer(source)

     if Player then
           exports['ghmattimysql']:execute('SELECT skills FROM players WHERE citizenid = @citizenid', {
               ['@citizenid'] = Player.PlayerData.citizenid
          }, function(status)
              if status ~= nil then
                   cb(json.decode(status))
              else
                   cb(nil)
              end
          end)
     else
          cb()
     end
end)
```


```lua
ESX.RegisterServerCallback("system:fetchStatus", function(source, cb)
    local src = source
    local user = ESX.GetPlayerFromId(src)


    local fetch = [[
         SELECT
              skills
         FROM
              users
         WHERE
              identifier = @identifier
    ]]

    MySQL.Async.fetchScalar(fetch, {
         ["@identifier"] = user.identifier

    }, function(status)

         if status ~= nil then
              cb(json.decode(status))
         else
              cb(nil)
         end

    end)
end)
```
-----------------------------------------------------------------------------------------------------------------------
```lua
QBCore.Functions.ExecuteSql()
```

```lua
ESX.ExecuteSql() --(ghmattimysql)
MySQL.Async.execute()
```
----------------------------------------------------------------------------------------------------------------------
QBCore.Commands.Add()
```lua
RegisterCommand 
```
-- (RegisterCommand qbcore'da da çalışır.)
----------------------------------------------------------------------------------------------------------------------
