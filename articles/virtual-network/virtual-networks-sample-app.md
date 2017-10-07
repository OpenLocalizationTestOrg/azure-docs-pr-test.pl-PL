---
title: "aaaAzure przykładowej aplikacji do użycia z sieci DMZ | Dokumentacja firmy Microsoft"
description: "Wdrażanie to prostą aplikację sieci web po utworzeniu DMZ tootest scenariusze przepływu ruchu"
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
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>Przykładowa aplikacja do użycia z sieci DMZ
[Zwraca toohello strony najlepsze rozwiązania w zakresie granic zabezpieczeń][HOME]

Można uruchomić lokalnie na powitania IIS01 i AppVM01 tooinstall serwerów i skonfigurować prostą aplikację sieci web wyświetlający stronę html, z serwerem frontonu IIS01 hello zawartością z serwera AppVM01 zaplecza hello te skrypty programu PowerShell.

Ta aplikacja zapewnia prostym środowisku testowym wiele hello przykłady DMZ i jak zmiany na hello punktów końcowych, grup NSG, przez i reguły zapory mogą mieć wpływ na ruch.

## <a name="firewall-rule-tooallow-icmp"></a>Tooallow reguł zapory ICMP
Proste niniejszych PowerShell można uruchomić na dowolny ruch protokołu ICMP (Ping) tooallow maszyny Wirtualnej systemu Windows. Ta aktualizacja zapora pozwala na łatwiejsze Rozwiązywanie problemów i testowanie zezwalając hello polecenia ping protokołu toopass przez zaporę systemu windows hello (w przypadku większości dystrybucjach systemu Linux, które ICMP jest domyślnie włączona).

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

Jeśli używasz hello następujące skrypty, to dodawanie reguły zapory jest hello pierwszej instrukcji.

## <a name="iis01---web-application-installation-script"></a>IIS01 - skrypt instalacji aplikacji sieci Web
Ten skrypt będzie:

1. Otwórz IMCPv4 (Ping) w Zaporze systemu windows serwer lokalny hello na łatwiejsze testowanie
2. Zainstaluj usługi IIS i hello .net Framework 4.5
3. Utwórz stronę sieci web ASP.NET i plik Web.config
4. Zmień hello domyślnej puli toomake pliku dostęp do aplikacji łatwiejsze
5. Ustaw hello anonimowego tooyour administratora konta użytkownika i hasło

Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie, gdy istniało RDP do IIS01.

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

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
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
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

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01 - skrypt instalacji serwera plików
Ten skrypt ustawia zaplecza hello Ta prosta aplikacja. Ten skrypt będzie:

1. Otwórz IMCPv4 (Ping) na zaporze hello na łatwiejsze testowanie
2. Utwórz katalog hello witryny sieci web
3. Utwórz toobe pliku tekstowego zdalnie dostęp przez stronę sieci web hello
4. Ustaw uprawnienia na powitania katalogów i plików tooAnonymous tooallow dostępu
5. Wyłącz tooallow zwiększonych zabezpieczeń programu Internet Explorer, ułatwia przeglądanie z tego serwera 

> [!IMPORTANT]
> **Najlepsze praktyki**: nigdy nie zostanie wyłączone zwiększonych zabezpieczeń programu Internet Explorer na serwerze produkcyjnym, a także ogólnie jest dobrym pomysłem toosurf hello sieci web na serwerze produkcyjnym. Otwarcie udziałów plików dla dostępu anonimowego jest również dobrym pomysłem, ale gotowe tutaj dla uproszczenia.
> 
> 

Ten skrypt programu PowerShell powinien zostać uruchomiony lokalnie, gdy istniało RDP do AppVM01. PowerShell jest wymagane toobe Uruchom jako Administrator tooensure pomyślne wykonanie.

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
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

## <a name="dns01---dns-server-installation-script"></a>DNS01 - skrypt instalacji serwera DNS
Nie ma żadnego skryptu zawarte w tej przykładowej tooset aplikacji hello serwera DNS. Jeśli testowania hello reguły zapory, NSG lub przez musi tooinclude ruch DNS, serwer hello DNS01 musi toobe skonfigurować ręcznie. plik xml konfiguracji sieci Hello i szablon Menedżera zasobów dla obu przykłady obejmuje DNS01 jako podstawowy serwer DNS hello i hello poziom 3 jako hello kopii zapasowej serwera DNS na użytek publiczny serwer DNS. Hello poziomu 3 serwer DNS może być hello używanego serwera DNS dla ruchu innego niż lokalne i z DNS01 nie Instalatora, nie sieci lokalnej, które wystąpiłyby DNS.

## <a name="next-steps"></a>Następne kroki
* Uruchom skrypt IIS01 hello na serwerze IIS
* Uruchom skrypt z serwera plików na AppVM01
* Przeglądaj toohello publicznego adresu IP na IIS01 toovalidate kompilacji

<!--Link References-->
[HOME]: ../best-practices-network-security.md
