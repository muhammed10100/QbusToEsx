# QbusToEsx Qbus Scriptleri ESX e Çevirme.
--------------------------------------------------------------------------------------------------
Qbus Temeli Ve ESX temeli.
 ```lua
QBCore = nil 

Citizen.CreateThread(function()
	while QBCore == nil do
		TriggerEvent('QBCore:GetObject', function(obj) QBCore = obj end)
		Citizen.Wait(30) -- Saniye Bekletme
	end
end)
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX = nil

Citizen.CreateThread(function()
  while ESX == nil do
    TriggerEvent('esx:getSharedObject', function(obj) ESX = obj end)
    Citizen.Wait(30)-- Saniye Bekletme
  end
end)
```
--------------------------------------------------------------------------------------------------
Oyuncu Giriş Kısmı İlik Oyuna Girerken Lazım, Yani Server Dosyasıdır.
```lua
RegisterNetEvent('QBCore:Client:OnPlayerLoaded')
AddEventHandler('QBCore:Client:OnPlayerLoaded', 
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:playerLoaded')
AddEventHandler('esx:playerLoaded',
```
--------------------------------------------------------------------------------------------------
Server Dosyası, Job Kısmı Meslek Kısmıdır.
```lua
RegisterNetEvent('QBCore:Client:OnJobUptade')
AddEventHandler('QBCore:Client:OnJobUptade', 
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:setJob')
AddEventHandler('esx:setJob',
```
--------------------------------------------------------------------------------------------------
Beyler Bu kısım Yoktu eklendi.
Anlamı:
Bu olay, oyuncu sunucuya bağlandığında tetiklenir
```lua
RegisterNetEvent('QBCore:Client:OnPlayerLoaded')
AddEventHandler('QBCore:Client:OnPlayerLoaded',
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
RegisterNetEvent('esx:playerLoaded')
AddEventHandler('esx:playerLoaded',
```
--------------------------------------------------------------------------------------------------
3D li Yazı Ekleme, Cilent Dosyası. Örnek : https://media.discordapp.net/attachments/623207764314816562/812096508786507806/resim_1.png
```lua
QBCore.Functions.DrawText3D(1, 1, 1, 'Örnek')
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
DrawText3D(1, 1, 1, 'Örnek') -- (aşağısına function açmanız gerekmektedir.)
```
--------------------------------------------------------------------------------------------------
Menu Aç Kapat ESX & QBCore De Ki Menüler Örnekler : https://prnt.sc/u4f7s5
```lua
QBCore.UI.Menu.Open
QBCore.UI.Menu.CloseAll() -- (menu default scripti kurmanız gerekmektedir.)
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.UI.Menu.Open
ESX.UI.Menu.CloseAll()
```
--------------------------------------------------------------------------------------------------
Bildirim Scripti Örnek : https://dosya.turkmmo.com/2020/09/36521_efa54848705a4069cbedfc2770e50cf1.png
```lua
QBCore.Functions.Notify("Araç kitlendi.", "error")
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
TriggerEvent('Notification',"Örnek.")
```
--------------------------------------------------------------------------------------------------
Enventer İtem Kısmı.
```lua
xPlayer.Functions.GetItemByName 
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
xPlayer.getInventoryItem
```
--------------------------------------------------------------------------------------------------
Para Ver Para Al Kısmı
```lua
ply.Functions.AddMoney('bank', amount, "Bank depost") -- banka
ply.Functions.RemoveMoney('cash', amount, "Bank depost") -- üstündeki para
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
xPlayer.removeAccountMoney('bank', amount) --para kaldırma
xPlayer.addMoney(amount) -- para ekleme
```
--------------------------------------------------------------------------------------------------
Para Kısmı Data.
```lua
ply.PlayerData.money["bank"]
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
xPlayer.getAccount('bank').money
```
--------------------------------------------------------------------------------------------------
Envanter İtem Silme Kısmı.
```lua
xPlayer.Functions.RemoveItem 
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
xPlayer.removeInventoryItem 
```
--------------------------------------------------------------------------------------------------
Envanter İtem Ekleme Kısmı.
```lua
xPlayer.Functions.AddItem
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
xPlayer.addInventoryItem
```
--------------------------------------------------------------------------------------------------
Karakter Kımsı Oyuncunun İd Si Gibi Birşey.
```lua
QBCore.Functions.GetPlayer(src)
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.GetPlayerFromId(src)
```
--------------------------------------------------------------------------------------------------
Araba Spawn Kısmı Konumu Vsb Şeyler.
```lua
QBCore.Functions.SpawnVehicle()
QBCore.Functions.GetVehicleProperties()
QBCore.Functions.GetClosestVehicle()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.Game.SpawnVehicle()
ESX.Game.GetVehicleProperties()
ESX.Game.GetClosestVehicle()
```
--(Eğer ESX.Game olan neredeyse her şey QBCore.Functions olarak aynı şekildedir.)
--------------------------------------------------------------------------------------------------
Oyuncu Kendi Karakterin.
```lua
QBCore.Functions.GetPlayerData()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.GetPlayerData()
```
--------------------------------------------------------------------------------------------------
İtem Oluşturma.
```lua
QBCore.Functions.CreateUseableItem()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.RegisterUsableItem()
```
--------------------------------------------------------------------------------------------------
Dosya'lar İle Alakalı.
```lua
QBCore.Functions.CreateCallback()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.RegisterServerCallback()
```
--------------------------------------------------------------------------------------------------
Dosya'lar İle Alakalı.
```lua
QBCore.Functions.TriggerCallback()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.TriggerServerCallback()
```
--------------------------------------------------------------------------------------------------
qb'de cid esx'de identifier kullanılıyor olayı çözmeniz için ufak bir kod bloğu bıraktım.
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
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
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
--------------------------------------------------------------------------------------------------
Sql bağlama kısmı
```lua
QBCore.Functions.ExecuteSql()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
ESX.ExecuteSql() --(ghmattimysql)
MySQL.Async.execute()
```
--------------------------------------------------------------------------------------------------
RegisterCommand - yani chat komut kısmı.
```lua
QBCore.Commands.Add()
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
RegisterCommand 
```
-- (RegisterCommand qbcore'da da çalışır.)
--------------------------------------------------------------------------------------------------
Karakter Kısmı Dır Data Sına Bağlama.
```lua
local Player = QBCore.Functions.GetPlayer(source)
['@citizenid'] = Player.PlayerData.citizenid
```
# ÜSTEKİ QBUSCORE

# ALTAKİ ESX
```lua
local user : ESX.Get.PlayerFromId(src)
["@identifier"] = user.identifier
```
--------------------------------------------------------------------------------------------------
