-- Fruit Luck Spin System (5x Luck)
-- Server-side only

local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- Create RemoteEvent if not exists
local spinEvent = ReplicatedStorage:FindFirstChild("SpinFruit")
if not spinEvent then
    spinEvent = Instance.new("RemoteEvent")
    spinEvent.Name = "SpinFruit"
    spinEvent.Parent = ReplicatedStorage
end

-- Fruit chances (base values)
local Fruits = {
    {Name = "Common Fruit", Chance = 60},
    {Name = "Rare Fruit", Chance = 25},
    {Name = "Legendary Fruit", Chance = 10},
    {Name = "Mythical Fruit", Chance = 5},
}

-- Give player luck
game.Players.PlayerAdded:Connect(function(player)
    local luck = Instance.new("NumberValue")
    luck.Name = "LuckMultiplier"
    luck.Value = 5 -- 🔥 5x luck
    luck.Parent = player
end)

-- Spin function
local function SpinFruit(player)
    local luck = player:FindFirstChild("LuckMultiplier").Value
    local totalChance = 0

    for _, fruit in pairs(Fruits) do
        totalChance += fruit.Chance * luck
    end

    local roll = math.random(1, totalChance)
    local current = 0

    for _, fruit in pairs(Fruits) do
        current += fruit.Chance * luck
        if roll <= current then
            return fruit.Name
        end
    end
end

-- When player spins
spinEvent.OnServerEvent:Connect(function(player)
    local result = SpinFruit(player)
    print(player.Name .. " spun and got: " .. result)
end)
