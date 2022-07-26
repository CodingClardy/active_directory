# 01 Installing the Domain Controller

1. Use `sconfig` to:
    - Change the hostname
    - Change the IP address to static
    - Change the DNS server to our own IP address

2.  Install the Active Directory Windows Feature

```shell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

- `import-Module ADDSDeployment`
- `Install-ADDSForest`

3. After AD install. It resets the server DNS IP to a loopback.
    - You can see this with `Get-DnsClientServerAddress`
    - Change with `Set-DnsClientServerAddress -InterfaceIndex x -ServerAddresses 192.168.153.155`


# 02 Setting up Management Client

1. 

2. With wanting to administer the DC from our Management Client, will be utilizing PowerShell Remote.
    - Adding the DC to our Management Client's trusted host so that we can `PSSession` to DC1 before joining the domain.
    - `Start-Service WinRM` 
    - `Get-Item wsman:\localhost\Client\TrustedHosts` (Should be blank)
    - `Set-Item wsman:\localhost\Client\TrustedHosts -value 192.168.153.155` (DC1 IPAddress)
    - `New-PSSession -ComputerName 192.168.153.155 -Credential (Get-Credential)`
    - `Enter-PSSession 1`

2. Setting up Chocolatey package manager
    `https://chocolatey.org/install`

3. Use Chocolately to install git and vscode for note taking. (I decided to skip this part as im taking notes on my host machine)

# 03 Setting up WS01

1. Cloned Win11 base with updates / VMWare tools to use as WS01
2. Change the DNS server
    - `Get-DnsClientServerAddress` to verify the interface indext
    - `Set-DnsClientServerAddress -InterfaceIndex x -ServerAddressess 192.168.153.155`
3. Joing the xyz.com domain
    - `Add-Computer -DomainName xyz.com -Credential xyz\Administrator -Restart -Force`
    