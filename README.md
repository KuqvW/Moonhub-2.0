local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "MoonHub", HidePremium = false, SaveConfig = true, ConfigFolder = "Moon Hub"})
local Tab = Window:MakeTab({
	Name = "Blatant",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})
local PlankForceamt = 0
local PlankForce = false
local aa = false
local aw = false

local m = Window:MakeTab({
	Name = "Misc",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddButton({
	Name = "Answer Question",
	Callback = function()
      		
	if   PlankForce == false and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion.Enabled == true  and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion.SubmitAlready.Value == false and  game:GetService("ReplicatedStorage").HintAnswer.Value ~= ""  then

local arg2 = string.len(game:GetService("ReplicatedStorage").HintAnswer.Value)

local args = {
    [1] = game:GetService("ReplicatedStorage").HintAnswer.Value,
    [2] = arg2
    



}

game:GetService("ReplicatedStorage").SubmittedAnswer:FireServer(unpack(args))
elseif  PlankForce == true and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion.Enabled == true  and game:GetService("Players").LocalPlayer.PlayerGui.TimeLeftQuestion.SubmitAlready.Value == false and  game:GetService("ReplicatedStorage").HintAnswer.Value ~= "" then
	local args = {
    [1] = game:GetService("ReplicatedStorage").HintAnswer.Value,
    [2] = PlankForceamt
    



}

game:GetService("ReplicatedStorage").SubmittedAnswer:FireServer(unpack(args))
	
      		        end
  	end    
})

m:AddDropdown({
	Name = "Plank Skin",
	Default = "blue",
	Options = {"blue", "red", "yellow", "green", "orange", "violet","pink","grey","white","black","rainbow","zigzag","zoom","space","crisscross","rose","spring","zebra","marble","achromatic","classic","lavender","blush","azure","dynamic","stitch","lush","jelly","spiderman","pastel","fall"},
	Callback = function(Value)
		local args = {
    [1] = Value
}

game:GetService("ReplicatedStorage").blockSkinFire:FireServer(unpack(args))

	end    
})
Tab:AddButton({
	Name = "Say Longest Possible Answer",
	Callback = function()
      		if game:GetService("ReplicatedStorage").HintAnswer.Value == "" then

      		    else
      		        local args = {
    [1] = "Longest Possible Answer Is ".. game:GetService("ReplicatedStorage").HintAnswer.Value,
    [2] = "All"
}

game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(unpack(args))

      		        end
  	end    
})
m:AddButton({
	Name = "Notify Longest Possible Answer",
	Callback = function()
      		if game:GetService("ReplicatedStorage").HintAnswer.Value == "" then
OrionLib:MakeNotification({
	Name = "Did Not Find An Answer",
	Content = "Please Try Again After There Is A Question",
	Image = "rbxassetid://4483345998",
	Time = 5
})
      		    else
      		        OrionLib:MakeNotification({
	Name = "Longest Possible Answer",
	Content = game:GetService("ReplicatedStorage").HintAnswer.Value,
	Image = "rbxassetid://4483345998",
	Time = 5
})

      		        end
  	end    
})


local WaterDisabled = false
m:AddToggle({
	Name = "In Game Spoofer",
	Default = false,
	Callback = function(ingametog)
	game:GetService("Players").LocalPlayer.Playing.Value = ingametog	
	end    
})
Tab:AddToggle({
	Name = "Disable Water",
	Default = false,
	Callback = function(WaterTog)
		WaterDisabled = WaterTog
	end    
})
Tab:AddToggle({
	Name = "Auto Win",
	Default = false,
	Callback = function(awtog)
	aw = awtog
	end    
})
Tab:AddToggle({
	Name = "Plank Force",
	Default = false,
	Callback = function(PlankForceToggle)
		PlankForce = PlankForceToggle
	end    
})
Tab:AddSlider({
	Name = "Plank Amount",
	Min = 0,
	Max = 10000000,
	Default = 20,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "Planks",
	Callback = function(PlankAmtSlider)
	PlankForceamt = PlankAmtSlider

	end    
})
local hook
hook = hookmetamethod(game, "__namecall", newcclosure(function(self, ...)
    local Args = {...}
   
    local method = getnamecallmethod()
    if PlankForce == true and  self.Name == "SubmittedAnswer" and method == "FireServer"  and not checkcaller() then

     if (Args[2]) then
         Args[2] = PlankForceamt
        

end;

       return hook(self, table.unpack(Args));

    end
    return hook(self, ...)
    
end))
local watertouch
game:GetService("RunService").Heartbeat:Connect(function()  if  game:GetService("Workspace"):FindFirstChild("Water") and WaterDisabled == true then

    game:GetService("Workspace").Water.Parent = game:GetService("Lighting")
    elseif game:GetService("Lighting"):FindFirstChild("Water") and WaterDisabled == false then
        game:GetService("Lighting").Water.Parent = game:GetService("Workspace")
end
end)
game:GetService("RunService").Heartbeat:Connect(function()
    if  aw == true and  game:GetService("Players").LocalPlayer.Character and  game:GetService("Players").LocalPlayer.Character.HumanoidRootPart then
        game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-217, 59, 110)
        end
    end)

  
OrionLib:Init()
