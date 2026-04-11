--// LocalScript → StarterPlayerScripts

local Players          = game:GetService("Players")
local StarterGui       = game:GetService("StarterGui")
local TweenService     = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

local player    = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- ────────────────────────────────────────────────
--  Create ScreenGui + UI
-- ────────────────────────────────────────────────
local sg = Instance.new("ScreenGui")
sg.Name = "OGBlockUI"
sg.ResetOnSpawn = false
sg.Parent = playerGui

local main = Instance.new("Frame")
main.Size       = UDim2.new(0, 220, 0, 150)
main.Position   = UDim2.new(0.5, -110, 0.5, -75)
main.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
main.BorderSizePixel = 0
main.ClipsDescendants = true
main.Parent = sg

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = main

local stroke = Instance.new("UIStroke")
stroke.Color      = Color3.fromRGB(255, 221, 85)
stroke.Thickness  = 2
stroke.Transparency = 0.45
stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
stroke.Parent = main

-- Title bar (draggable)
local titleBar = Instance.new("Frame")
titleBar.Size               = UDim2.new(1, 0, 0, 34)
titleBar.BackgroundTransparency = 1
titleBar.Parent = main

local title = Instance.new("TextLabel")
title.Size               = UDim2.new(1, 0, 1, 0)
title.BackgroundTransparency = 1
title.Font               = Enum.Font.GothamBold
title.Text               = "OG BLOCK"
title.TextColor3         = Color3.fromRGB(255, 221, 85)
title.TextSize           = 20
title.TextStrokeTransparency = 0.75
title.TextStrokeColor3   = Color3.new(0,0,0)
title.Parent = titleBar

-- Credit label removed completely
-- (wala na yung "Made By Mark L." sa UI)

-- Big button
local btn = Instance.new("TextButton")
btn.Name = "InjectButton"
btn.Size       = UDim2.new(0.88, 0, 0, 54)
btn.Position   = UDim2.new(0.06, 0, 0, 62)
btn.BackgroundColor3 = Color3.fromRGB(255, 190, 40)
btn.TextColor3       = Color3.fromRGB(22, 22, 26)
btn.Font             = Enum.Font.GothamBlack
btn.Text             = "OG BLOCK"
btn.TextSize         = 26
btn.AutoButtonColor  = false
btn.Parent = main

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 9)
btnCorner.Parent = btn

local btnStroke = Instance.new("UIStroke")
btnStroke.Color      = Color3.fromRGB(255, 221, 85)
btnStroke.Thickness  = 2.5
btnStroke.Transparency = 0.35
btnStroke.Parent = btn

local UIGrad = Instance.new("UIGradient")
UIGrad.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0.0, Color3.fromRGB(255,240,140)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255,190,40)),
    ColorSequenceKeypoint.new(1.0, Color3.fromRGB(255,240,140)),
}
UIGrad.Rotation = 35
UIGrad.Parent = btn

-- ────────────────────────────────────────────────
--  Draggable
-- ────────────────────────────────────────────────
local dragging, dragStart, startPos

titleBar.InputBegan:Connect(function(input)
    if not (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then return end
    
    dragging   = true
    dragStart  = input.Position
    startPos   = main.Position
    
    input.Changed:Connect(function()
        if input.UserInputState == Enum.UserInputState.End then
            dragging = false
        end
    end)
end)

UserInputService.InputChanged:Connect(function(input)
    if not dragging then return end
    if not (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then return end
    
    local delta = input.Position - dragStart
    main.Position = UDim2.new(
        startPos.X.Scale,   startPos.X.Offset + delta.X,
        startPos.Y.Scale,   startPos.Y.Offset + delta.Y
    )
end)

-- ────────────────────────────────────────────────
--  Button animations
-- ────────────────────────────────────────────────
local function tween(obj, props, time, style)
    TweenService:Create(obj, TweenInfo.new(time or 0.25, style or Enum.EasingStyle.Quint), props):Play()
end

btn.MouseEnter:Connect(function()
    tween(btn,       {BackgroundColor3 = Color3.fromRGB(255, 215, 80)}, 0.25)
    tween(btnStroke, {Transparency = 0.1}, 0.25)
    tween(UIGrad,    {Rotation = 70}, 0.8)
end)

btn.MouseLeave:Connect(function()
    tween(btn,       {BackgroundColor3 = Color3.fromRGB(255, 190, 40)}, 0.25)
    tween(btnStroke, {Transparency = 0.35}, 0.25)
    tween(UIGrad,    {Rotation = 35}, 0.8)
end)

btn.MouseButton1Down:Connect(function()
    tween(btn, {Size = UDim2.new(0.84, 0, 0, 50)}, 0.11)
end)

btn.MouseButton1Up:Connect(function()
    tween(btn, {Size = UDim2.new(0.88, 0, 0, 54)}, 0.2, Enum.EasingStyle.Back)
end)

-- ────────────────────────────────────────────────
--  REAL INJECT LOGIC
-- ────────────────────────────────────────────────
local alreadyInjected = false

local function notify(text)
    StarterGui:SetCore("SendNotification", {
        Title = "OG Block",
        Text = text,   -- walang credit
        Duration = 5,
    })
end

local function tryMakeOG(block)
    if not block:IsA("TextLabel") then return false end
    
    local parent = block.Parent
    if not parent then return false end
    
    local display = parent:FindFirstChild("DisplayName")
    if not (display and display:IsA("TextLabel") and display.Text == "Lucky Block") then
        return false
    end
    
    local changed = false
    
    if block.Text == "Secret" then
        block.Text = "OG"
        block.TextColor3 = Color3.fromRGB(255, 221, 85)
        
        if not block:FindFirstChildOfClass("UIStroke") then
            local st = Instance.new("UIStroke")
            st.Color = Color3.new(0,0,0)
            st.Thickness = 2
            st.Parent = block
        end
        
        local grad = block:FindFirstChildOfClass("UIGradient")
        if grad then
            grad.Color = ColorSequence.new{
                ColorSequenceKeypoint.new(0,   Color3.fromRGB(255,235,120)),
                ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255,190,50)),
                ColorSequenceKeypoint.new(1,   Color3.fromRGB(255,235,120)),
            }
        end
        
        changed = true
        
    elseif block.Text == "$750M" then
        block.Text = "$750B"
        changed = true
    end
    
    return changed
end

local function injectNow()
    if alreadyInjected then
        notify("Already injected!")
        return
    end
    
    local count = 0
    
    -- Existing ones
    for _, v in ipairs(game:GetDescendants()) do
        if tryMakeOG(v) then
            count += 1
        end
    end
    
    -- Future ones
    game.DescendantAdded:Connect(function(child)
        task.spawn(function()
            if tryMakeOG(child) then
                count += 1
            end
        end)
    end)
    
    alreadyInjected = true
    
    if count > 0 then
        notify("Injected → Found and upgraded " .. count .. " Secret block(s)")
    else
        notify("No Secret Lucky Blocks found in current game")
    end
end

-- Button action
btn.Activated:Connect(function()
    local oldText = btn.Text
    btn.Text = "Injecting..."
    tween(btn, {BackgroundColor3 = Color3.fromRGB(90, 200, 90)}, 0.15)
    
    task.delay(0.9, function()
        injectNow()
        
        btn.Text = oldText
        tween(btn, {BackgroundColor3 = Color3.fromRGB(255, 190, 40)}, 0.35)
    end)
end)

notify("UI Loaded • Drag from top • Press button to activate OG blocks"); okBtn.BorderSizePixel = 0; okBtn.Text = "OK"
    okBtn.TextColor3 = Color3.fromRGB(18,18,18); okBtn.Font = Enum.Font.GothamBold
    okBtn.TextSize = 17; okBtn.ZIndex = 22
    Instance.new("UICorner", okBtn).CornerRadius = UDim.new(0,10)

    cancelBtn.MouseEnter:Connect(function() TweenService:Create(cancelBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(58,58,70)}):Play() end)
    cancelBtn.MouseLeave:Connect(function() TweenService:Create(cancelBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(42,42,52)}):Play() end)
    okBtn.MouseEnter:Connect(function() TweenService:Create(okBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(215,215,215)}):Play() end)
    okBtn.MouseLeave:Connect(function() TweenService:Create(okBtn,TweenInfo.new(0.1),{BackgroundColor3=Color3.fromRGB(240,240,240)}):Play() end)

    local closing=false; local fillDone=false; local buyDone=false; local fillTween=nil

    local function closeDown()
        if closing then return end; closing=true
        if fillTween then fillTween:Cancel() end
        TweenService:Create(card,TweenInfo.new(0.32,Enum.EasingStyle.Quint,Enum.EasingDirection.In),{Position=UDim2.new(0.5,0,1.4,0)}):Play()
        TweenService:Create(overlay,TweenInfo.new(0.30),{BackgroundTransparency=1}):Play()
        task.delay(0.33,function() screenGui:Destroy() end)
    end
    local function closeSuccess()
        if closing then return end; closing=true
        TweenService:Create(sCard,TweenInfo.new(0.32,Enum.EasingStyle.Quint,Enum.EasingDirection.In),{Position=UDim2.new(0.5,0,1.4,0)}):Play()
        TweenService:Create(overlay,TweenInfo.new(0.30),{BackgroundTransparency=1}):Play()
        task.delay(0.33,function() screenGui:Destroy() end)
    end
    local function showSuccess()
        card.Visible=false; sCard.Visible=true; sCard.Position=UDim2.new(0.5,0,-0.35,0)
        TweenService:Create(sCard,TweenInfo.new(0.38,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Position=UDim2.new(0.5,0,0.5,0)}):Play()
        pcall(function()
            local successSfx = game:GetService("ReplicatedStorage").Sounds.Sfx.Success
            successSfx:Play()
        end)
        if giftedTo and giftedTo ~= "" then
            if CoreGui:FindFirstChild("GiftLabelGUI") then
                CoreGui.GiftLabelGUI:Destroy()
            end
            local gGui = Instance.new("ScreenGui")
            gGui.Name           = "GiftLabelGUI"
            gGui.ResetOnSpawn   = false
            gGui.IgnoreGuiInset = true
            gGui.DisplayOrder   = 1000
            gGui.Parent         = CoreGui

            local gLabel = Instance.new("TextLabel", gGui)
            gLabel.Size                   = UDim2.new(1,0,0,40)
            gLabel.AnchorPoint            = Vector2.new(0.5,1)
            gLabel.Position               = UDim2.new(0.5,0,1,-64)
            gLabel.BackgroundTransparency = 1
            gLabel.RichText               = true
            gLabel.Text                   = '<font color="#92FF67">Successfully Gifted To '..giftedTo..'</font>'
            gLabel.Font                   = Enum.Font.GothamBold
            gLabel.TextSize               = 19
            gLabel.TextXAlignment         = Enum.TextXAlignment.Center
            gLabel.ZIndex                 = 5

            task.delay(5, function()
                if not gGui or not gGui.Parent then return end
                for i = 1, 20 do
                    task.wait(0.05)
                    if gLabel and gLabel.Parent then
                        gLabel.TextTransparency = i / 20
                    end
                end
                pcall(function() gGui:Destroy() end)
            end)

            screenGui.AncestryChanged:Connect(function()
                if not screenGui.Parent then
                    pcall(function() gGui:Destroy() end)
                end
            end)
        end
    end

    local slideTween=TweenService:Create(card,TweenInfo.new(0.42,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Position=UDim2.new(0.5,0,0.5,0)})
    slideTween:Play()
    slideTween.Completed:Connect(function()
        if closing then return end
        robuxIco.TextColor3=Color3.fromRGB(255,255,255)
        buyPriceLabel.TextColor3=Color3.fromRGB(255,255,255)
        fillTween=TweenService:Create(fillBar,TweenInfo.new(1.5,Enum.EasingStyle.Linear),{Size=UDim2.new(1,0,1,0)})
        fillTween:Play()
        fillTween.Completed:Connect(function(state)
            if state~=Enum.PlaybackState.Completed or closing then return end
            fillDone=true
            TweenService:Create(fillBar,TweenInfo.new(0.2),{BackgroundTransparency=1}):Play()
            TweenService:Create(robuxIco,TweenInfo.new(0.15),{TextColor3=Color3.fromRGB(18,18,18)}):Play()
            TweenService:Create(buyPriceLabel,TweenInfo.new(0.15),{TextColor3=Color3.fromRGB(18,18,18)}):Play()
        end)
    end)

    cancelBtn.MouseButton1Click:Connect(function() closeDown() end)
    buyBtn.MouseButton1Click:Connect(function()
        if not fillDone or buyDone or closing then return end
        buyDone=true; showSuccess()
    end)
    okBtn.MouseButton1Click:Connect(function() closeSuccess() end)
    overlay.InputBegan:Connect(function(inp)
        if inp.UserInputType==Enum.UserInputType.MouseButton1 then
            if sCard.Visible then closeSuccess() else closeDown() end
        end
    end)
end

local function injectItem(item)
    if item:FindFirstChild("__inj") then return end

    local buyObj = item:FindFirstChild("Buy")
    if not buyObj then return end

    local priceLbl    = buyObj:FindFirstChild("Price") or item:FindFirstChild("Price")
    local nameLbl     = item:FindFirstChild("ItemName") or item:FindFirstChild("Text")
    local iconObj     = item:FindFirstChild("Icon")

    local itemName    = (nameLbl  and nameLbl.Text)  or "Unknown"
    local itemPrice   = (priceLbl and priceLbl.Text) or "0"
    local itemImageId = (iconObj  and iconObj.Image) or ""

    local ghost = Instance.new("TextButton", buyObj)
    ghost.Name                   = "GhostBtn"
    ghost.Size                   = UDim2.new(1,0,1,0)
    ghost.Position               = UDim2.new(0,0,0,0)
    ghost.AnchorPoint            = Vector2.new(0,0)
    ghost.BackgroundTransparency = 1
    ghost.Text                   = ""
    ghost.AutoButtonColor        = false
    ghost.BorderSizePixel        = 0
    ghost.ZIndex                 = buyObj.ZIndex + 20

    local tag = Instance.new("BoolValue", item)
    tag.Name = "__inj"

    ghost.MouseButton1Click:Connect(function()
        local snd = Instance.new("Sound", game:GetService("SoundService"))
        snd.SoundId = "rbxassetid://75311202481026"
        snd.Volume = 1
        snd:Play()
        game:GetService("Debris"):AddItem(snd, 5)

        local giftedTo = nil
        pcall(function()
            local giftBtn = game:GetService("Players").LocalPlayer.PlayerGui.Shop.Shop.GiftPlayerSelect.Buttons.GiftButton
            local txt = giftBtn:FindFirstChild("Txt")
            if txt and txt:IsA("TextLabel") then
                if string.lower(txt.Text) == "back" then
                    local playerNameLbl = game:GetService("Players").LocalPlayer.PlayerGui.Shop.Shop.GiftPlayerSelect.PlayerSelected.PlayerName
                    if playerNameLbl then
                        local ct = playerNameLbl:FindFirstChild("ContentText") or playerNameLbl
                        giftedTo = ct.Text
                    end
                end
            end
        end)

        createBuyUI(itemName, itemPrice, itemImageId, giftedTo)
    end)
end

local function injectContainer(container, label)
    for _, child in ipairs(container:GetChildren()) do
        if child:IsA("ImageLabel") or child:IsA("Frame") then
            pcall(injectItem, child)
        end
    end
    container.ChildAdded:Connect(function(child)
        task.wait(0.1)
        if child:IsA("ImageLabel") or child:IsA("Frame") then
            pcall(injectItem, child)
        end
    end)
end

local function injectAll()
    local shopGui = playerGui:FindFirstChild(player.DisplayName..".Shop")
                 or playerGui:FindFirstChild(player.Name..".Shop")
                 or playerGui:FindFirstChild("Shop")

    if not shopGui then return end

    local inner   = shopGui:FindFirstChild("Shop")
    local content = inner  and inner:FindFirstChild("Content")
    local list    = content and content:FindFirstChild("List")

    if not list then return end

    local itemsList = list:FindFirstChild("ItemsList")
    if itemsList then
        injectContainer(itemsList, "ItemsList")
    end

    local gamepassList = list:FindFirstChild("GamepassList")
    if gamepassList then
        injectContainer(gamepassList, "GamepassList")

        local main = gamepassList:FindFirstChild("Main")
        if main then
            injectContainer(main, "GamepassList.Main")
        end
    end

    local serverLuck = list:FindFirstChild("ServerLuck")
    if serverLuck then
        local slFrame = serverLuck:FindFirstChild("Frame")
        if slFrame then
            pcall(injectItem, slFrame)
        end
        serverLuck.ChildAdded:Connect(function(child)
            task.wait(0.1)
            if child.Name == "Frame" then
                pcall(injectItem, child)
            end
        end)
    end
end

pcall(function()
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title    = "Successfully Injected | discord.gg/crustyhub",
        Text     = "Successfully Injected To Gears And Passes",
        Duration = 5,
    })
end)

task.spawn(function()
    local names = {player.DisplayName..".Shop", player.Name..".Shop", "Shop"}
    local found, waited = false, 0
    repeat
        task.wait(0.5); waited += 0.5
        for _,n in ipairs(names) do
            if playerGui:FindFirstChild(n) then found=true; break end
        end
    until found or waited >= 20
    if not found then return end
    task.wait(0.3)
    injectAll()
end)
