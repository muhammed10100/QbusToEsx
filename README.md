# QbusToEsx

QBCore = nil 

Citizen.CreateThread(function()
	while QBCore == nil do
		TriggerEvent('QBCore:GetObject', function(obj) QBCore = obj end)
		Citizen.Wait(31)
	end
end)


ESX = nil

Citizen.CreateThread(function()
  while ESX == nil do
    TriggerEvent('esx:getSharedObject', function(obj) ESX = obj end)
    Citizen.Wait(31)
  end
end)
-----------------------------------------------------------
RegisterNetEvent('QBCore:Client:OnPlayerLoaded')
AddEventHandler('QBCore:Client:OnPlayerLoaded', 
    
  RegisterNetEvent('esx:playerLoaded')
AddEventHandler('esx:playerLoaded',   
--------------------------------------------------------------------
RegisterNetEvent('QBCore:Client:OnJobUptade')
AddEventHandler('QBCore:Client:OnJobUptade', 

RegisterNetEvent('esx:setJob')
AddEventHandler('esx:setJob',
---------------------------------------------------------------------
QBCore.Functions.DrawText3D(1, 1, 1, 'Örnek')

DrawText3D(1, 1, 1, 'Örnek') -- (aşağısına function açmanız gerekmektedir.)
--------------------------------------------------------------------------------
QBCore.UI.Menu.Open
QBCore.UI.Menu.CloseAll() -- (menu default scripti kurmanız gerekmektedir.)

ESX.UI.Menu.Open
ESX.UI.Menu.CloseAll()
----------------------------------------------------------------------------------------
QBCore.Functions.Notify("Araç kitlendi.", "error")

TriggerEvent('Notification',"Örnek.")
----------------------------------------------------------------------------------------
xPlayer.Functions.GetItemByName 

xPlayer.getInventoryItem
---------------------------------------------------------------------------------------
xPlayer.Functions.RemoveItem 

xPlayer.removeInventoryItem 
-------------------------------------------------------------------------------------------
xPlayer.Functions.AddItem

xPlayer.addInventoryItem
----------------------------------------------------------------------------------------
QBCore.Functions.GetPlayer(src)

ESX.GetPlayerFromId(src)
--------------------------------------------------------------------------------------------------
QBCore.Functions.SpawnVehicle()
QBCore.Functions.GetVehicleProperties()
QBCore.Functions.GetClosestVehicle()


ESX.Game.SpawnVehicle()
ESX.Game.GetVehicleProperties()
ESX.Game.GetClosestVehicle()

--(Eğer ESX.Game olan neredeyse her şey QBCore.Functions olarak aynı şekildedir.)
------------------------------------------------------------------------------------------------------
QBCore.Functions.GetPlayerData()

ESX.GetPlayerData()
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
-- qb'de cid esx'de identifier kullanılıyor olayı çözmeniz için ufak bir kod bloğu bıraktık.
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
-----------------------------------------------------------------------------------------------------------------------
QBCore.Functions.ExecuteSql()

ESX.ExecuteSql() --(ghmattimysql)
MySQL.Async.execute()
----------------------------------------------------------------------------------------------------------------------
QBCore.Commands.Add()

RegisterCommand 
-- (RegisterCommand qbcore'da da çalışır.)
----------------------------------------------------------------------------------------------------------------------
