--If you are going to use to share out to the public credit me you skid. - noketchupjustrice#3666
--Everything should be fixed was just debating wether I should release this or not.
if not game:IsLoaded() then
	game.IsLoaded:Wait()
end;

local Players = game:service("Players")
local LocalPlayer = Players.LocalPlayer

if not LocalPlayer.Character then
	repeat task.wait() until LocalPlayer.Character
end;

local CheckInstance = function(Part)
	if Part.ClassName:lower():find("part") then
		local BaseInstance = Part;
		pcall(function()
			for i, Part in pairs(LocalPlayer.Character:GetDescendants()) do
				if Part.ClassName:lower():find("part") then
					local NoCollisionConstraint = Instance.new("NoCollisionConstraint", BaseInstance)
					NoCollisionConstraint.Enabled = true
					NoCollisionConstraint.Part0 = BaseInstance;
					NoCollisionConstraint.Part1 = Part;
				end
			end
		end)
	end
end;

local Insert = function(Target, Bool)
	local Start = function()
		local Inserted = {}
		if not Target.Character then
			Target.CharacterAdded:Wait()
		end;
		Target.Character:WaitForChild("Head", 5)
		Target.Character:WaitForChild("Humanoid", 5)
		spawn(function()
			pcall(function()
				for i, v in pairs(Target.Character:GetDescendants()) do
					if v:IsA("NoCollisionConstraint") then
						v:Destroy()
					end
				end;
				for i, v in pairs(Target.Character:GetDescendants()) do
					CheckInstance(v)
				end;
				Target.Character.DescendantAdded:Connect(function(v)
					if not table.find(Inserted, v) then
						table.insert(Inserted, v)
						CheckInstance(v)
					end
				end)
			end)
		end)
	end;
	pcall(Start)
	if not Bool then
		Target.CharacterAdded:Connect(Start)
	end
end;

for i, v in pairs(Players:GetPlayers()) do
	if v ~= LocalPlayer then
		Insert(v, false)
	end
end;

Players.PlayerAdded:Connect(Insert, false)

local Reset = function()
	if not LocalPlayer.Character then
		LocalPlayer.CharacterAdded:Wait()
	end;
	LocalPlayer.Character:WaitForChild("Head")
	LocalPlayer.Character:WaitForChild("Humanoid")
	for i, v in pairs(Players:GetPlayers()) do
		if v ~= LocalPlayer then
			pcall(function()
				for i, v in pairs(v.Character:GetDescendants()) do
					if v.IsA(v, "NoCollisionConstraint") then
						v:Destroy()
					end
				end
			end)
			Insert(v, true)
		end
	end
end;

LocalPlayer.CharacterAdded:Connect(Reset)
