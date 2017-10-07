---
title: "aaaConfiguring projektu platformy Azure przy użyciu konfiguracji z wieloma usługi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure platformy Azure w chmurze projekt usługi, zmieniając hello ServiceDefinition.csdef i pliku ServiceConfiguration.cscfg plików."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Konfigurowanie projektu platformy Azure przy użyciu wielu konfiguracji usługi
Projekt usługi w chmurze Azure zawiera dwa pliki konfiguracji: ServiceDefinition.csdef i pliku ServiceConfiguration.cscfg. Pliki te są spakować z aplikacją usługi chmury Azure i wdrożone tooAzure.

* Witaj **ServiceDefinition.csdef** plik zawiera hello metadanych, które jest wymagane przez hello środowiska platformy Azure na potrzeby hello aplikacji usługi chmury, łącznie z ról, które zawiera. Ten plik zawiera także ustawienia konfiguracji, które są stosowane tooall wystąpień. Te ustawienia konfiguracji mogą być odczytywane w czasie wykonywania za pomocą hello obsługującego środowisko uruchomieniowe interfejsu API usługi Azure. Nie można zaktualizować tego pliku, gdy usługa jest uruchomiona na platformie Azure.
* Witaj **pliku ServiceConfiguration.cscfg** plik ustawia wartości ustawienia konfiguracji hello zdefiniowane w pliku definicji usługi hello i określa hello liczbę wystąpień toorun dla każdej roli. Ten plik może zostać zaktualizowana uruchomionej usługi w chmurze na platformie Azure.

Hello Azure Tools dla programu Microsoft Visual Studio Podaj strony właściwości, których można użyć ustawień konfiguracji tooset przechowywanych w tych plikach. tooaccess hello strony właściwości, kliknij dwukrotnie odwołanie do roli hello poniżej projekt usługi w chmurze Azure hello w Eksploratorze rozwiązań, lub kliknij prawym przyciskiem myszy odwołanie do roli hello i wybierz **właściwości**, jak pokazano w powitania po rysunku.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Informacje hello bazowy schematów dla definicji usługi hello i pliki konfiguracji usługi, zobacz hello [odwołanie do schematu](https://msdn.microsoft.com/library/azure/dd179398.aspx). Aby uzyskać więcej informacji na temat konfiguracji usługi, zobacz [jak usług w chmurze tooConfigure](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Konfigurowanie właściwości roli
Witaj strony właściwości dla roli sieci web i roli proces roboczy są podobne, chociaż występują niewielkie różnice, wskazano w hello następujące sekcje.

Z hello **buforowanie** strony, można skonfigurować hello buforowanie usług Azure.

### <a name="configuration-page"></a>Na stronie konfiguracji
Na powitania **konfiguracji** stronę, można ustawić następujące właściwości:

**Wystąpienia**

Zestaw hello **wystąpienia** liczbę właściwości toohello wystąpień usługi hello powinno być ono uruchomione dla tej roli.

Hello zestaw **rozmiar maszyny Wirtualnej** właściwości zbyt**dodatkowe małych**, **małych**, **średni**, **duży**, lub **Bardzo dużych**.  Aby uzyskać więcej informacji, zobacz [rozmiary dla usług w chmurze](cloud-services/cloud-services-sizes-specs.md).

**Akcja uruchamiania** (rola sieci Web tylko)

Ustaw toospecify tej właściwości, które Visual Studio należy uruchomić przeglądarki sieci web dla punktów końcowych hello HTTP lub punktów końcowych HTTPS hello lub zarówno po rozpoczęciu debugowania.

Hello opcji punkt końcowy HTTPS jest dostępna tylko wtedy, gdy punkt końcowy HTTPS został już zdefiniowany dla roli użytkownika. Punkt końcowy HTTPS można zdefiniować na powitania **punkty końcowe** strony właściwości.

Jeśli masz już dodany punkt końcowy HTTPS, hello opcji punkt końcowy HTTPS jest domyślnie włączona i Visual Studio spowoduje uruchomienie przeglądarki dla tego punktu końcowego, po rozpoczęciu debugowania dodatkowo tooa przeglądarki dla punktu końcowego HTTP. Przy założeniu, że obie opcje uruchamiania są włączone.

**Diagnostyka**

Domyślnie diagnostyki jest włączone dla roli sieci Web hello. Hello projekt usługi w chmurze platformy Azure i konta magazynu są ustawiane toouse hello lokalnym emulatorze magazynu. Gdy wszystko jest gotowe toodeploy tooAzure, można wybrać przycisk konstruktora hello (**...** ) tooupdate hello magazynu konta toouse magazynu Azure w chmurze hello. Konto magazynu toohello hello diagnostyki danych można przenieść na żądanie lub automatycznie zaplanowanymi interwałami. Aby uzyskać więcej informacji na temat diagnostycznych platformy Azure, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Ustawienia strony
Na powitania **ustawienia** strony, można dodać ustawienia konfiguracji dla usługi. Ustawienia konfiguracji są pary nazwa wartość. Kod uruchomiony w roli hello może odczytywać hello wartości ustawień konfiguracji w czasie wykonywania za pomocą klasy podał hello [biblioteki zarządzane Azure](http://go.microsoft.com/fwlink?LinkID=171026). W szczególności hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) metoda zwraca wartość hello nazwane ustawienia w czasie wykonywania.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Konfigurowanie konta magazynu tooa ciąg połączenia
Ciąg połączenia jest ustawienie konfiguracji, które zawiera informacje o połączenia i uwierzytelniania dla emulatora magazynu hello lub dla konta magazynu platformy Azure. Zawsze, gdy kod muszą uzyskać dostęp do danych usługi Azure storage — oznacza to, obiektów blob, kolejki lub tabeli danych — od kodu działającego w roli, trzeba będzie toodefine ciąg połączenia dla tego konta magazynu.

Parametry połączenia, które wskazuje tooan kontem magazynu platformy Azure musi mieć format zdefiniowany. Aby uzyskać informacje na temat toocreate parametry połączenia, zobacz [skonfigurować parametry połączenia magazynu Azure](storage/common/storage-configure-connection-string.md).

Gdy są gotowe tootest usługi dla usług Azure storage hello, lub po gotowe toodeploy Twojego tooAzure usługi chmury, można zmienić wartości hello żadnych tooyour toopoint ciągów połączenia kontem magazynu platformy Azure. Wybierz (**...** ), wybierz pozycję **wprowadź poświadczenia konta magazynu**. Wprowadź informacje o Twoim koncie, która zawiera nazwę konta i klucz konta. W hello **parametry połączenia konta magazynu** okno dialogowe, można również określić opcję punktów końcowych HTTPS domyślnej hello toouse (opcja domyślna hello), końcowych HTTP domyślne hello lub niestandardowe punkty końcowe. Możesz określić niestandardowe punkty końcowe toouse Jeśli zarejestrowano niestandardowej nazwy domeny dla usługi, zgodnie z opisem w [Konfigurowanie niestandardowej nazwy domeny dla danych obiektów blob na koncie magazynu Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Należy zmodyfikować tooan toopoint Twojego połączenia ciągi kontem magazynu platformy Azure przed wdrożeniem usługi. W przypadku braku toodo może to spowodować roli użytkownika nie toostart lub toocycle za pośrednictwem hello inicjowania zajęty i zatrzymywanie stanów.
> 
> 

## <a name="endpoints-page"></a>Strona punkty końcowe
Rola proces roboczy może mieć dowolną liczbę punktów końcowych HTTP, HTTPS lub TCP. Punkty końcowe można wejściowych punktów końcowych, które są dostępne tooexternal klientów, lub wewnętrznych punktów końcowych, które są dostępne tooother ról, które działają w usłudze hello.

* toomake HTTP punktu końcowego dostępne tooexternal klienci przeglądarki sieci Web, zmień hello punktu końcowego typu tooinput i określ nazwę i numer portu publicznego.
* toomake HTTPS klientów dostępne tooexternal punktu końcowego i przeglądarki sieci Web, Zmień typ punktu końcowego hello zbyt**wejściowych**i określ nazwę, numer portu publicznego i nazwę certyfikatu zarządzania.
  
    Należy pamiętać, że zanim można będzie określić certyfikat zarządzania, należy zdefiniować certyfikat hello na powitania **certyfikaty** strony właściwości.
* toomake punkt końcowy dostępna wewnętrzny przez inne role hello w usłudze w chmurze, zmień hello punktu końcowego typu toointernal i określ nazwę i możliwe prywatnych portów dla tego punktu końcowego.

## <a name="local-storage-page"></a>Strona magazynu lokalnego
Można użyć hello **Magazyn lokalny** tooreserve strony właściwości, jeden lub więcej zasobów magazynu lokalnego dla roli. Zasób magazynu lokalnego jest katalogiem zastrzeżonego w systemie plików hello hello maszyny wirtualnej platformy Azure, w którym działa wystąpienie roli.

## <a name="certificates-page"></a>Strona Certyfikaty
Na powitania **certyfikaty** strony, certyfikaty można skojarzyć z roli użytkownika. Możesz dodać, może być używane tooconfigure punktów końcowych HTTPS na powitania certyfikatom Hello **punkty końcowe** strony właściwości.

Witaj **certyfikaty** strony właściwości dodaje informacje o konfiguracji usługi tooyour certyfikatów. Należy pamiętać, że certyfikaty nie są dostarczane z usługą; należy przekazać certyfikaty oddzielnie tooAzure za pośrednictwem hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate certyfikatu z roli użytkownika, podaj nazwę hello certyfikatu. Użyj tego certyfikatu toohello toorefer nazwy podczas konfigurowania punktu końcowego HTTPS hello **punkty końcowe** strony właściwości. Następnie określ, czy magazyn certyfikatów hello jest **komputera lokalnego** lub **bieżącego użytkownika** i nazwę hello hello magazynu. Na koniec wprowadź odcisk palca certyfikatu hello. Jeśli certyfikat hello hello User\Personal bieżącego magazynu (Mój), można wprowadzić hello odcisk palca certyfikatu, wybierając hello certyfikatu z listy wypełnione. Jeśli znajduje się ona w innej lokalizacji, wprowadź wartość odcisku palca hello ręcznie.

Po dodaniu certyfikatu z magazynu certyfikatów hello wszelkie certyfikaty pośrednie są automatycznie dodawane toohello ustawienia konfiguracji dla Ciebie. Te certyfikaty pośrednie, należy również przekazać tooAzure w kolejności toocorrectly skonfigurować usługi dla protokołu SSL.

Wszystkie certyfikaty zarządzania skojarzonych z usługą mają zastosowanie usługi tooyour tylko wtedy, gdy jest uruchomiona w chmurze hello. Gdy usługa jest uruchomiona w hello lokalne Środowisko deweloperskie, używa to standardowy certyfikat, który jest zarządzany przez emulator obliczeń hello.

## <a name="configuring-hello-azure-cloud-service-project"></a>Konfigurowanie projektu usługi w chmurze Azure hello
Ustawienia tooconfigure dotyczące projektu usługi chmury Azure cały tooan, pierwszym otwarciu hello menu skrótów dla tego węzła projektu, a następnie wybierz właściwości tooopen stron jej właściwości. Witaj w poniższej tabeli przedstawiono te strony właściwości.

| Strony właściwości | Opis |
| --- | --- |
| Aplikacja |Na tej stronie można wyświetlić informacje o wersji hello narzędzi Azure, która używa tego projektu usługi w chmurze, a uaktualnieniem toohello bieżącej wersji narzędzi hello. |
| Zdarzenia kompilacji |Na tej stronie można ustawić zdarzenia prekompilacyjnego i mające miejsce po kompilacji. |
| Opracowywanie zawartości |Na tej stronie można określić instrukcje konfiguracji kompilacji i hello warunków, w których są uruchamiane wszystkie zdarzenia postkompilacyjnego. |
| Sieć Web |Na tej stronie można skonfigurować ustawienia, które dotyczą toohello serwera sieci web. |

