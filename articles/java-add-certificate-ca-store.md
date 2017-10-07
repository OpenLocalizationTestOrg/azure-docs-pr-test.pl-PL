---
title: "Magazyn certyfikatów urzędu certyfikacji Java toohello aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd certyfikatu urzędu certyfikacji certyfikatu toohello Java certyfikat urzędu certyfikacji (cacerts) przechowywania dla usługi usługi Twilio lub usługi Azure Service Bus."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Dodawanie certyfikatu toohello magazynu certyfikatów urzędu certyfikacji Java
Hello następujące kroki pokazują, jak tooadd certyfikatu urzędu certyfikacji certyfikatu toohello Java certyfikat urzędu certyfikacji (cacerts) przechowywania. przykład Witaj używany jest hello urzędu certyfikacji certyfikatu wymagany przez hello usługi usługi Twilio. Informacje podane w dalszej części tematu hello opisano, jak hello tooinstall urzędu certyfikacji certyfikatu dla hello Azure Service Bus. 

Można użyć keytool tooadd hello urzędu certyfikacji certyfikatu przed toozipping Twojego JDK i dodać go tooyour projektu platformy Azure **approot** folderze, lub można uruchomić zadanie uruchamiania Azure korzystającej z certyfikatu hello tooadd keytool. W tym przykładzie przyjęto założenie, że dodasz toohello wcześniejszego certyfikatu JDK trwa zip urzędu certyfikacji. Ponadto określonego certyfikatu urzędu certyfikacji będzie używany w przykład Witaj, ale kroki hello uzyskania innego certyfikatu urzędu certyfikacji i importowanie hello cacerts magazynu mogą być podobne.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>przechowywanie cacerts toohello certyfikatu tooadd
1. W wierszu polecenia ustawionej tooyour JDK **jdk\jre\lib\security** folderu Uruchom powitania po toosee, jakie są zainstalowane:
   
    `keytool -list -keystore cacerts`
   
    Zostanie wyświetlony monit o hasło sklepu hello. Witaj domyślne hasło jest **changeit**. (Jeśli chcesz toochange hello hasła, zobacz dokumentację keytool hello w <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) W tym przykładzie założono tego certyfikatu hello z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 nie ma na liście, i ma tooimport it (tego konkretnego certyfikatu jest wymagane przez hello usługi interfejsu API usługi Twilio).
2. Uzyskiwanie certyfikatu hello z listy hello certyfikatów wymienione na [certyfikaty główne GeoTrust](http://www.geotrust.com/resources/root-certificates/). Kliknij prawym przyciskiem myszy łącze hello hello certyfikatu z 35:DE:F4:CF numer seryjny i zapisaniu toohello **jdk\jre\lib\security** folderu. Do celów tego przykładu, została zapisana tooa plik o nazwie **firmy Equifax\_bezpiecznego\_certyfikatu\_Authority.cer**.
3. Zaimportuj certyfikat hello za pośrednictwem hello następujące polecenie:
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Gdy monit tootrust tego certyfikatu, jeśli certyfikat hello zawiera MD5 odcisk palca 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, Odpowiedz, wpisując **y**.
4. Hello uruchom następujące polecenie tooensure hello urzędu certyfikacji certyfikat został pomyślnie zaimportowany:
   
    `keytool -list -keystore cacerts`
5. Pliku zip hello JDK i dodać go tooyour Azure projektu **approot** folderu.

Aby uzyskać informacje o keytool, zobacz <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certyfikaty główne Azure
Aplikacji, które korzystają z usług Azure (np. usługi Azure Service Bus), wymagany jest certyfikat główny firmy CyberTrust Baltimore hello tootrust. (Począwszy od 15 kwietnia 2013 Azure rozpoczynająca się migrowania hello GTE CyberTrust Root globalne toohello Baltimore CyberTrust Root. Ta migracja trwało kilka toocomplete miesięcy).

Hello Baltimore certyfikatu może być zainstalowany w magazynie cacerts więc Pamiętaj toorun hello **keytool — lista** polecenia toosee pierwszy, jeśli już istnieje.

Jeśli potrzebujesz tooadd hello Baltimore CyberTrust Root, ma numer seryjny 02:00:00:b9 i SHA1 odcisk palca d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74. Można go pobrać z <https://cacert.omniroot.com/bc2025.crt>, zapisany z rozszerzeniem pliku lokalnego tooa **.cer**, a następnie zaimportowane przy użyciu **keytool** zgodnie z powyższym.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello certyfikaty główne używane przez usługę Azure, zobacz [migracji certyfikatu głównego Azure](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Aby uzyskać więcej informacji na temat języka Java, zobacz [Azure dla deweloperów języka Java](/java/azure).

