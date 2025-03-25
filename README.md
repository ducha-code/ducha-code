local player = game.Players.LocalPlayer
local camera = game.Workspace.CurrentCamera
local runService = game:GetService("RunService")
local lockedPart = workspace:WaitForChild("Part")  -- The part you want the camera to lock onto

-- Optional: Adjust the camera's offset
local offset = Vector3.new(0, 5, -10)  -- Customize the offset as needed

local function lockCamera()
    -- Lock camera position and orientation to the selected part
    camera.CameraType = Enum.CameraType.Scriptable
    
    -- Update the camera's position each frame
    runService.RenderStepped:Connect(function()
        camera.CFrame = CFrame.new(lockedPart.Position + offset, lockedPart.Position)
    end)
end

local function unlockCamera()
    -- Reset the camera to default behavior
    camera.CameraType = Enum.CameraType.Custom
Toggle camera lock when the user presses the 'X' key
player.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.X then
        if camera.CameraType == Enum.CameraType.Scriptable then
            unlockCamera()
        else
            lockCamera()
        end
    end
end)
