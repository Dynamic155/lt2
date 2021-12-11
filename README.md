local function SendNotification(Title,Text,Duration) -- Sends Notification in the bottom right of the screen
	game.StarterGui:SetCore("SendNotification", {
		Title = Title;
		Text = Text;
		Icon = nil;
		Duration = Duration
	})
end
 
DMoney.Name = "DMoney"
DMoney.Parent = CopyFrame
DMoney.BackgroundColor3 = Color3.new(0, 0, 0)
DMoney.BorderColor3 = Color3.new(0, 0, 0)
DMoney.Position = UDim2.new(0, 3, 0, 302)
DMoney.Size = UDim2.new(0, 90, 0, 20)
DMoney.Font = Enum.Font.Fantasy
DMoney.FontSize = Enum.FontSize.Size18
DMoney.Text = "Dupe Money"
DMoney.TextColor3 = Color3.new(255, 0, 0)
DMoney.TextSize = 15
DMoney.MouseButton1Down:connect(function() --Sends the money and will come back after around 2 mins
	if MoneyCooldown == true then
		SendNotification("Cooldown Notification", "Wait for your Money to come back",2)
		return
	elseif MoneyCooldown == false then
		MoneyCooldown = true
		SendNotification("Money Sent", "Wait about 2 minutes for your Money to come back", 5)
		game.ReplicatedStorage.Transactions.ClientToServer.Donate:InvokeServer(game.Players.LocalPlayer, game.Players.LocalPlayer.leaderstats.Money.Value, 1)
		SendNotification("Money Received", "You received your money that you have sent earlier", 5)
		MoneyCooldown = false
	end
end)
