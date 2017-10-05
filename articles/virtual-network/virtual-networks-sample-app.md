---
title: "Azure przykładowej aplikacji do użycia z sieci DMZ | Dokumentacja firmy Microsoft"
description: "Wdrażanie to prostą aplikację sieci web po utworzeniu strefą DMZ do testowania scenariuszy przepływu ruchu"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 8506238e41c5d9dac8d76d729d4919b30a0528b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="e56c8-103">Przykładowa aplikacja do użycia z sieci DMZ</span><span class="sxs-lookup"><span data-stu-id="e56c8-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="e56c8-104">[Wróć do strony zabezpieczeń granic najlepsze praktyki][HOME]</span><span class="sxs-lookup"><span data-stu-id="e56c8-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="e56c8-105">Te skrypty programu PowerShell można uruchomić lokalnie na serwerach IIS01 i AppVM01, aby zainstalować i skonfigurować prostą aplikację sieci web wyświetlający stronę html, na serwerze frontonu IIS01 zawartością z wewnętrznego serwera AppVM01.</span><span class="sxs-lookup"><span data-stu-id="e56c8-105">These PowerShell scripts can be run locally on the IIS01 and AppVM01 servers to install and set up a simple web application that displays an html page from the front-end IIS01 server with content from the back-end AppVM01 server.</span></span>

<span data-ttu-id="e56c8-106">Ta aplikacja zawiera prostym środowisku testowym dla wielu przykłady DMZ i w jaki sposób zmiany punktów końcowych, grup NSG, przez i zapory reguły mogą mieć wpływ na ruch.</span><span class="sxs-lookup"><span data-stu-id="e56c8-106">This application provides a simple testing environment for many of the DMZ Examples and how changes on the Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-to-allow-icmp"></a><span data-ttu-id="e56c8-107">Reguły zapory, aby umożliwić protokołu ICMP</span><span class="sxs-lookup"><span data-stu-id="e56c8-107">Firewall rule to allow ICMP</span></span>
<span data-ttu-id="e56c8-108">Proste niniejszych PowerShell można uruchomić na dowolnej maszyny Wirtualnej systemu Windows, aby zezwolić na ruch protokołu ICMP (Ping).</span><span class="sxs-lookup"><span data-stu-id="e56c8-108">This simple PowerShell statement can be run on any Windows VM to allow ICMP (Ping) traffic.</span></span> <span data-ttu-id="e56c8-109">Ta aktualizacja zapory umożliwia łatwiejsze Rozwiązywanie problemów i testowanie, zezwalając na polecenie ping protokołu przekazywanie przez zaporę systemu windows (w przypadku większości dystrybucjach systemu Linux, które ICMP jest domyślnie włączona).</span><span class="sxs-lookup"><span data-stu-id="e56c8-109">This firewall update allows for easier testing and troubleshooting by allowing the ping protocol to pass through the windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="e56c8-110">Korzystając z poniższych skryptów, to dodawanie reguły zapory jest pierwszą instrukcją.</span><span class="sxs-lookup"><span data-stu-id="e56c8-110">If you use the following scripts, this firewall rule addition is the first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="e56c8-111">IIS01 - skrypt instalacji aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="e56c8-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="e56c8-112">Ten skrypt będzie:</span><span class="sxs-lookup"><span data-stu-id="e56c8-112">This script will:</span></span>

1. <span data-ttu-id="e56c8-113">Otwórz IMCPv4 (Ping) na lokalny serwer zapory systemu windows na łatwiejsze testowanie</span><span class="sxs-lookup"><span data-stu-id="e56c8-113">Open IMCPv4 (Ping) on the local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="e56c8-114">Instalacja usług IIS i platformy .net Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="e56c8-114">Install IIS and the .Net Framework v4.5</span></span>
3. <span data-ttu-id="e56c8-115">Utwórz stronę sieci web ASP.NET i plik Web.config</span><span class="sxs-lookup"><span data-stu-id="e56c8-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="e56c8-116">Zmiana domyślnej puli aplikacji, aby ułatwić dostęp do plików</span><span class="sxs-lookup"><span data-stu-id="e56c8-116">Change the Default application pool to make file access easier</span></span>
5. <span data-ttu-id="e56c8-117">Ustaw użytkownika anonimowego do konta administratora i hasła</span><span class="sxs-lookup"><span data-stu-id="e56c8-117">Set the Anonymous user to your admin account and password</span></span>

<span data-ttu-id="e56c8-118">Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie, gdy istniało RDP do IIS01.</span><span class="sxs-lookup"><span data-stu-id="e56c8-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter the admin account information used to create this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "The Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "The Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from the inside (a web server on a private network),<br />
          and it is making its way to the outside! (If you are viewing this from the internet)<br />
          <br />
          The following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that the web server is reaching AppVM01 on the backend subnet and successfully returning content</li>
            <li> Image from the Internet - Doesnt really show anything, but it made me happy to see this when the app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from the Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool to Clasic Pipeline to remote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure the IIS settings take
    Write-Host "Restarting the W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="e56c8-119">AppVM01 - skrypt instalacji serwera plików</span><span class="sxs-lookup"><span data-stu-id="e56c8-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="e56c8-120">Ten skrypt konfiguruje wewnętrzną Ta prosta aplikacja.</span><span class="sxs-lookup"><span data-stu-id="e56c8-120">This script sets up the back-end for this simple application.</span></span> <span data-ttu-id="e56c8-121">Ten skrypt będzie:</span><span class="sxs-lookup"><span data-stu-id="e56c8-121">This script will:</span></span>

1. <span data-ttu-id="e56c8-122">Otwórz IMCPv4 (Ping) na łatwiejsze testowanie zapory</span><span class="sxs-lookup"><span data-stu-id="e56c8-122">Open IMCPv4 (Ping) on the firewall for easier testing</span></span>
2. <span data-ttu-id="e56c8-123">Utwórz katalog dla witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="e56c8-123">Create a directory for the web site</span></span>
3. <span data-ttu-id="e56c8-124">Utwórz plik tekstowy zdalnie za dostęp przez stronę sieci web</span><span class="sxs-lookup"><span data-stu-id="e56c8-124">Create a text file to be remotely access by the web page</span></span>
4. <span data-ttu-id="e56c8-125">Ustawianie uprawnień dla katalogu i pliku anonimowy, aby zezwolić na dostęp</span><span class="sxs-lookup"><span data-stu-id="e56c8-125">Set permissions on the directory and file to Anonymous to allow access</span></span>
5. <span data-ttu-id="e56c8-126">Wyłącz zwiększone zabezpieczenia programu Internet Explorer umożliwia łatwiejsze przeglądanie z tego serwera</span><span class="sxs-lookup"><span data-stu-id="e56c8-126">Turn off IE Enhanced Security to allow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e56c8-127">**Najlepsze praktyki**: nigdy nie zostanie wyłączone zwiększonych zabezpieczeń programu Internet Explorer na serwerze produkcyjnym, a także ogólnie jest dobrym pomysłem przeglądać sieć web na serwerze produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e56c8-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea to surf the web from a production server.</span></span> <span data-ttu-id="e56c8-128">Otwarcie udziałów plików dla dostępu anonimowego jest również dobrym pomysłem, ale gotowe tutaj dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="e56c8-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="e56c8-129">Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie, gdy istniało RDP do AppVM01.</span><span class="sxs-lookup"><span data-stu-id="e56c8-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="e56c8-130">PowerShell jest wymagany do uruchamiania jako Administrator, aby zapewnić pomyślne wykonanie.</span><span class="sxs-lookup"><span data-stu-id="e56c8-130">PowerShell is required to be run as Administrator to ensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands to work

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm the contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="e56c8-131">DNS01 - skrypt instalacji serwera DNS</span><span class="sxs-lookup"><span data-stu-id="e56c8-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="e56c8-132">Nie ma żadnego skryptu zawarte w tej przykładowej aplikacji, aby skonfigurować serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="e56c8-132">There is no script included in this sample application to set up the DNS server.</span></span> <span data-ttu-id="e56c8-133">Podczas testowania reguł zapory, NSG lub przez musi zawierać ruch DNS, serwera DNS01 musi zostać można skonfigurować ręcznie.</span><span class="sxs-lookup"><span data-stu-id="e56c8-133">If testing of the firewall rules, NSG, or UDR needs to include DNS traffic, the DNS01 server needs to be set up manually.</span></span> <span data-ttu-id="e56c8-134">Plik xml konfiguracji sieci i szablonu usługi Resource Manager zarówno przykłady zawiera DNS01 jako podstawowy serwer DNS i publiczny serwer DNS w obsługiwanych przez poziom 3 jako kopii zapasowej serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e56c8-134">The Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as the primary DNS server and the public DNS server hosted by Level 3 as the backup DNS server.</span></span> <span data-ttu-id="e56c8-135">Poziom 3 serwer DNS może być używanego serwera DNS dla ruchu innego niż lokalne i z DNS01 nie Instalatora, nie sieci lokalnej, które wystąpiłyby DNS.</span><span class="sxs-lookup"><span data-stu-id="e56c8-135">The Level 3 DNS server would be the actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e56c8-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e56c8-136">Next steps</span></span>
* <span data-ttu-id="e56c8-137">Uruchom skrypt IIS01 na serwerze IIS</span><span class="sxs-lookup"><span data-stu-id="e56c8-137">Run the IIS01 script on an IIS server</span></span>
* <span data-ttu-id="e56c8-138">Uruchom skrypt z serwera plików na AppVM01</span><span class="sxs-lookup"><span data-stu-id="e56c8-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="e56c8-139">Przejdź do publicznego adresu IP na IIS01 do weryfikacji kompilacji</span><span class="sxs-lookup"><span data-stu-id="e56c8-139">Browse to the Public IP on IIS01 to validate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
