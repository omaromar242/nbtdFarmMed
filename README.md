local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer
local remotes = ReplicatedStorage:WaitForChild("Remotes")
local events = remotes:WaitForChild("Events")
local functions = remotes:WaitForChild("Functions")

-- --- Helper Function: Wait for Coin Value ---
local function waitForCoins(amount)
    local leaderstats = player:WaitForChild("leaderstats")
    local coins = leaderstats:WaitForChild("Coins")
    
    -- Yields the script until you have enough money
    while coins.Value < amount do
        task.wait(0.5)
    end
end

-- --- Main Automation Sequence ---

-- 1. Initial Game Setup
task.wait(6)
events.Ready:FireServer()

task.wait(4)
events.Gamemode:FireServer("Medium")

task.wait(5)
events.InitChangeSpeed:FireServer(2)

-- 2. Place First Tower (1x1x1x1)
functions.PlaceTower:InvokeServer({
    ["towerToPlace"] = "1x1x1x1",
    ["instance"] = workspace.Map.Map.Baseplate.Placeable.Part,
    ["towerID"] = "43205fb2-04e4-49e5-8820-f100afa16ed1",
    ["position"] = Vector3.new(-4.724559783935547, 0.049997709691524506, 7.969427108764648),
})

-- Upgrades for Tower 1
waitForCoins(750)
functions.UpgradeTower:InvokeServer("1")

waitForCoins(1200)
functions.UpgradeTower:InvokeServer("1")

-- 3. Place Railgunner (Tower 2)
waitForCoins(3000)
functions.PlaceTower:InvokeServer({
    ["towerToPlace"] = "Railgunner",
    ["instance"] = workspace.Map.Map.Baseplate.Placeable.Part,
    ["towerID"] = "2adbf692-0081-4e73-abc9-943e00266b07",
    ["position"] = Vector3.new(-0.6966552734375, 0.04999961704015732, 3.4951295852661133),
})

-- More Upgrades for Tower 1
waitForCoins(1500)
functions.UpgradeTower:InvokeServer("1")

waitForCoins(2000)
functions.UpgradeTower:InvokeServer("1")

-- Upgrades for Tower 2
waitForCoins(2600)
functions.UpgradeTower:InvokeServer("2")

waitForCoins(5600)
functions.UpgradeTower:InvokeServer("2")

-- 4. Place Second 1x1x1x1 (Tower 3)
waitForCoins(400)
functions.PlaceTower:InvokeServer({
    ["towerToPlace"] = "1x1x1x1",
    ["instance"] = workspace.Map.Map.Baseplate.Placeable.Part,
    ["towerID"] = "43205fb2-04e4-49e5-8820-f100afa16ed1",
    ["position"] = Vector3.new(-4.6674394607543945, 0.04999866336584091, 10.55978012084961),
})

-- Upgrades for Tower 3
waitForCoins(750)
functions.UpgradeTower:InvokeServer("3")

waitForCoins(1200)
functions.UpgradeTower:InvokeServer("3")

waitForCoins(1450)
functions.UpgradeTower:InvokeServer("3")

waitForCoins(2000)
functions.UpgradeTower:InvokeServer("3")

-- 5. Final Tower 2 Upgrades
waitForCoins(9600)
functions.UpgradeTower:InvokeServer("2")

waitForCoins(16000)
functions.UpgradeTower:InvokeServer("2")
