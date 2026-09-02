
```lua
--// Auto R Toggle
--// Nhấn R để BẬT/TẮT tự động nhấn R
--// Không giữ phím R

local UserInputService = game:GetService("UserInputService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local StarterGui = game:GetService("StarterGui")

local enabled = false
local delayTime = 0.1 -- thời gian giữa mỗi lần nhấn R

local function notify(text)
    StarterGui:SetCore("SendNotification", {
        Title = "Auto R",
        Text = text,
        Duration = 2
    })
end

local function pressR()
    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.R, false, game)
    task.wait(0.03)
    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.R, false, game)
end

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end

    if input.KeyCode == Enum.KeyCode.R then
        enabled = not enabled

        if enabled then
            notify("ĐÃ BẬT Auto R")
            
            task.spawn(function()
                while enabled do
                    pressR()
                    task.wait(delayTime)
                end
            end)
        else
            notify("ĐÃ TẮT Auto R")
        end
    end
end)

notify("Nhấn R để bật Auto R")
```
