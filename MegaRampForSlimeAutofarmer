local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local running = false

local OpenBox = ReplicatedStorage.Remotes.OpenBoxClick


local function StartBoxClick()
    task.spawn(function()
        while running do
            OpenBox:FireServer()
            task.wait(0.05)
        end
    end)
end


local function StartLoop()
    while running do

        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        -- Spieler teleportieren
        character:PivotTo(CFrame.new(0, 125, -1540))
        task.wait(0.4)

        -- Auto setzen
        local car = workspace[player.Name .. "_Auto1"]
        car:PivotTo(
            CFrame.new(0, 75, -1305) *
            CFrame.Angles(0, math.rad(180), 0)
        )

        task.wait(0.3)

        -- Auto bewegen
        local start = car:GetPivot()
        local target = CFrame.new(0, 20, 2800)

        local steps = 150
        local time = 0.5

        for i = 1, steps do
            if not running then return end

            local alpha = i / steps
            car:PivotTo(start:Lerp(target, alpha))
            task.wait(time / steps)
        end


        -- Ab hier dauerhaft Boxen klicken
        StartBoxClick()


        task.wait(5)
    end
end


UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end

    if input.KeyCode == Enum.KeyCode.F then

        running = not running

        if running then
            print("AUTO START")
            task.spawn(StartLoop)
        else
            print("AUTO STOP")
        end
    end
end)