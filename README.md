-- ئەمە "Loader"ـەکەیە بۆ
local scriptText = [[
-- GUI بۆ دوگمەی Vip free
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "VIP_Kill_Gui"
screenGui.Parent = game:GetService("CoreGui")

local button = Instance.new("TextButton")
button.Name = "VIP_Kill_Button"
button.Parent = screenGui
button.Size = UDim2.new(0, 150, 0, 50)
button.Position = UDim2.new(0.5, -75, 0.8, 0)
button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
button.BackgroundTransparency = 0.3
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.Text = "Vip free"
button.Font = Enum.Font.GothamBold
button.TextSize = 14

local closeBtn = Instance.new("TextButton")
closeBtn.Name = "Close"
closeBtn.Parent = screenGui
closeBtn.Size = UDim2.new(0, 20, 0, 20)
closeBtn.Position = UDim2.new(0.5, 135, 0.8, 0)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 12

local function executeVIPKill()
    local workspace = game:GetService("Workspace")
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer
    
    local function findAllVIPKill()
        local found = {}
        for _, obj in ipairs(workspace:GetDescendants()) do
            if obj.Name and (obj.Name == "VIP Kill" or obj.Name == "VIPKill" or obj.Name:match("VIP.*Kill")) then
                table.insert(found, obj)
            end
        end
        return found
    end
    
    local function findVIPSpawm()
        for _, obj in ipairs(workspace:GetDescendants()) do
            if obj.Name and (obj.Name == "VIP Spawn" or obj.Name == "VIPSpawn" or obj.Name:match("VIP.*Spawn")) then
                return obj
            end
        end
        return nil
    end
    
    local vipKillObjects = findAllVIPKill()
    if #vipKillObjects > 0 then
        for _, obj in ipairs(vipKillObjects) do
            obj:Destroy()
        end
    end
    
    local character = localPlayer.Character
    if not character or not character.Parent then
        character = localPlayer.CharacterAdded:Wait()
    end
    
    local hrp = character:WaitForChild("HumanoidRootPart", 2)
    local spawnPoint = findVIPSpawm()
    
    if spawnPoint and hrp then
        hrp.CFrame = spawnPoint.CFrame
    end
end

button.MouseButton1Click:Connect(function()
    executeVIPKill()
    button.Text = "✅ Done!"
    task.wait(1)
    button.Text = "Vip free"
end)

closeBtn.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

print("✅ Vip free - User: Muhammad0909096")
]]

loadstring(scriptText)()
