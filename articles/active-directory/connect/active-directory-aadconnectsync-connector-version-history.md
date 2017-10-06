---
title: aaaConnector Historia wersji | Dokumentacja firmy Microsoft
description: "W tym temacie wymieniono wszystkie wersje hello łączników dla programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="e1495-103">Historia wersji łącznika</span><span class="sxs-lookup"><span data-stu-id="e1495-103">Connector Version Release History</span></span>
<span data-ttu-id="e1495-104">Witaj łączników programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM) są często aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="e1495-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="e1495-105">Ten temat dotyczy tylko programu FIM i MIM.</span><span class="sxs-lookup"><span data-stu-id="e1495-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="e1495-106">Te łączniki nie są obsługiwane dla instalacji na Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e1495-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="e1495-107">Łączniki wydanej jest preinstalowany na AADConnect podczas uaktualniania toospecified kompilacji.</span><span class="sxs-lookup"><span data-stu-id="e1495-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="e1495-108">Ten temat zawiera wszystkie wersje hello łączniki, które zostały wydane.</span><span class="sxs-lookup"><span data-stu-id="e1495-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="e1495-109">Linki pokrewne:</span><span class="sxs-lookup"><span data-stu-id="e1495-109">Related links:</span></span>

* [<span data-ttu-id="e1495-110">Pobierz najnowsze łączników</span><span class="sxs-lookup"><span data-stu-id="e1495-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="e1495-111">[Ogólny łącznik LDAP](active-directory-aadconnectsync-connector-genericldap.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e1495-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="e1495-112">[Ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e1495-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="e1495-113">[Łącznik usług Web](http://go.microsoft.com/fwlink/?LinkID=226245) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e1495-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="e1495-114">[Łącznik programu PowerShell](active-directory-aadconnectsync-connector-powershell.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e1495-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="e1495-115">[Łącznika programu Lotus Domino](active-directory-aadconnectsync-connector-domino.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="e1495-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="e1495-116">1.1.604.0 (AADConnect do czasu zwolnienia)</span><span class="sxs-lookup"><span data-stu-id="e1495-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="e1495-117">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="e1495-117">Fixed issues:</span></span>

* <span data-ttu-id="e1495-118">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="e1495-118">Generic Web Services:</span></span>
  * <span data-ttu-id="e1495-119">Rozwiązano problem uniemożliwia tworzone podczas wystąpiły co najmniej dwa punkty końcowe projektu protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="e1495-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="e1495-120">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="e1495-120">Generic SQL:</span></span>
  * <span data-ttu-id="e1495-121">W operacji hello importu hello GSQL został nie konwertowania czasu poprawnie, po zapisaniu tooconnector miejsca.</span><span class="sxs-lookup"><span data-stu-id="e1495-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="e1495-122">Witaj domyślny format daty i godziny dla przestrzeni łącznika hello GSQL został zmieniony z "RRRR MM-dd: ssZ" too'yyyy-MM-dd: ssZ ".</span><span class="sxs-lookup"><span data-stu-id="e1495-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="e1495-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="e1495-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="e1495-124">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="e1495-124">Fixed issues:</span></span>

* <span data-ttu-id="e1495-125">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="e1495-125">Generic Web Services:</span></span>
  * <span data-ttu-id="e1495-126">Narzędzie Wsconfig Hello nie zostały przekonwertowane poprawnie hello tablicy Json z "przykładowe żądanie" dla metody usługi REST hello.</span><span class="sxs-lookup"><span data-stu-id="e1495-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="e1495-127">Przyczyną problemów z serializacji tej tablicy Json dla żądania REST hello.</span><span class="sxs-lookup"><span data-stu-id="e1495-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="e1495-128">Narzędzie konfiguracji łącznika usług sieci Web nie obsługuje użycia miejsca symboli w nazwach atrybutów JSON</span><span class="sxs-lookup"><span data-stu-id="e1495-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="e1495-129">Wzorzec podstawienia mogą być dodawane ręcznie toohello WSConfigTool.exe.config pliku, np.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="e1495-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="e1495-130">Program Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="e1495-130">Lotus Notes:</span></span>
  * <span data-ttu-id="e1495-131">Gdy hello opcja **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** jest wyłączona, a następnie hello łącznika kończy się niepowodzeniem podczas eksportu (aktualizacji), po eksportu hello przepływu wszystkie atrybuty są tooDomino wyeksportowany, ale w czasie hello Eksport KeyNotFoundException jest zwracana tooSync.</span><span class="sxs-lookup"><span data-stu-id="e1495-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="e1495-132">Zdarza się to hello zmienić operacja kończy się niepowodzeniem podczas próby toochange nazwa Wyróżniająca (atrybut nazwy użytkownika), zmieniając jeden z atrybutów hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="e1495-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="e1495-133">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="e1495-133">LastName</span></span>
      - <span data-ttu-id="e1495-134">Imię</span><span class="sxs-lookup"><span data-stu-id="e1495-134">FirstName</span></span>
      - <span data-ttu-id="e1495-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="e1495-135">MiddleInitial</span></span>
      - <span data-ttu-id="e1495-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="e1495-136">AltFullName</span></span>
      - <span data-ttu-id="e1495-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="e1495-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="e1495-138">jednostki organizacyjnej</span><span class="sxs-lookup"><span data-stu-id="e1495-138">ou</span></span>
      - <span data-ttu-id="e1495-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="e1495-139">altcommonname</span></span>

  * <span data-ttu-id="e1495-140">Gdy **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** opcja jest włączona, ale wydających świadectwa wymagane są nadal puste, a następnie KeyNotFoundException występuje.</span><span class="sxs-lookup"><span data-stu-id="e1495-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="e1495-141">Ulepszenia:</span><span class="sxs-lookup"><span data-stu-id="e1495-141">Enhancements:</span></span>

* <span data-ttu-id="e1495-142">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="e1495-142">Generic SQL:</span></span>
  * <span data-ttu-id="e1495-143">**Scenariusz: przeprojektowany implementowany:** "*" funkcji</span><span class="sxs-lookup"><span data-stu-id="e1495-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="e1495-144">**Opis rozwiązania:** zmienić podejście do [Obsługa atrybuty wielowartościowe odwołanie](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="e1495-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="e1495-145">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="e1495-145">Fixed issues:</span></span>

* <span data-ttu-id="e1495-146">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="e1495-146">Generic Web Services:</span></span>
  * <span data-ttu-id="e1495-147">Nie można zaimportować konfigurację serwera, jeśli znajduje się łącznik usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="e1495-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="e1495-148">Łącznik usługi sieci Web nie działa z wieloma usługami sieci Web</span><span class="sxs-lookup"><span data-stu-id="e1495-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="e1495-149">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="e1495-149">Generic SQL:</span></span>
  * <span data-ttu-id="e1495-150">Brak typów obiektu są wyświetlane pojedynczą wartość atrybutu do którego istnieje odwołanie</span><span class="sxs-lookup"><span data-stu-id="e1495-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="e1495-151">Import zmian śledzenia zmian wartość zostanie usunięty z tabeli wielowartościowych obiektu usuwa strategii</span><span class="sxs-lookup"><span data-stu-id="e1495-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="e1495-152">Overflowexception — w łączniku GSQL z bazy danych DB2 na AS / 400</span><span class="sxs-lookup"><span data-stu-id="e1495-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="e1495-153">Program Lotus:</span><span class="sxs-lookup"><span data-stu-id="e1495-153">Lotus:</span></span>
  * <span data-ttu-id="e1495-154">Dodano opcję tooenable\disable wyszukiwanie jednostki organizacyjne przed otwarciem GlobalParameters strony</span><span class="sxs-lookup"><span data-stu-id="e1495-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="e1495-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="e1495-155">1.1.443.0</span></span>

<span data-ttu-id="e1495-156">Wydanie: 2017 marca</span><span class="sxs-lookup"><span data-stu-id="e1495-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="e1495-157">Ulepszenia</span><span class="sxs-lookup"><span data-stu-id="e1495-157">Enhancements</span></span>

* <span data-ttu-id="e1495-158">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="e1495-158">Generic SQL:</span></span></br><span data-ttu-id="e1495-159">
  **Scenariusz symptomy:** jest dobrze znane ograniczenie z hello łącznik SQL, w którym możemy tylko Zezwalaj typu obiektu tooone odwołania i wymagają odwołań z elementami członkowskimi.</span><span class="sxs-lookup"><span data-stu-id="e1495-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="e1495-160">
**Opis rozwiązania:** w kroku przetwarzania hello odwołań "*" zostanie wybrana opcja, wszystkich kombinacji typów obiektów, zostanie zwrócony wstecz toohello aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e1495-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="e1495-161">Spowoduje to utworzenie wielu symboli zastępczych</span><span class="sxs-lookup"><span data-stu-id="e1495-161">This will create many placeholders</span></span>
- <span data-ttu-id="e1495-162">Jest wymagane toomake się, że nazewnictwa hello jest unikatowa między typami obiektów.</span><span class="sxs-lookup"><span data-stu-id="e1495-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="e1495-163">Ogólny LDAP:</span><span class="sxs-lookup"><span data-stu-id="e1495-163">Generic LDAP:</span></span></br><span data-ttu-id="e1495-164">
 **Scenariusz:** po wybraniu kilku kontenerów w określonej partycji, następnie wyszukiwania hello nadal będzie realizowane w całej partycji.</span><span class="sxs-lookup"><span data-stu-id="e1495-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="e1495-165">Właściwe będą filtrowane przez usługę synchronizacji, ale nie MA, co może spowodować obniżenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="e1495-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="e1495-166">**Opis rozwiązania:** łącznik GLDAP zmienić kod toomake możliwe przechodzi przez wszystkie kontenery i wyszukiwania obiektów w każdej z nich, zamiast wyszukiwanie w całej partycji hello.</span><span class="sxs-lookup"><span data-stu-id="e1495-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="e1495-167">Programu Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="e1495-167">Lotus Domino:</span></span>

  <span data-ttu-id="e1495-168">**Scenariusz:** Domino poczty usunięcia obsługę usunięcie osoby podczas eksportowania.</span><span class="sxs-lookup"><span data-stu-id="e1495-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="e1495-169">
  **Rozwiązanie:** obsługi usuwania można skonfigurować poczty do usunięcia osoby, podczas eksportowania.</span><span class="sxs-lookup"><span data-stu-id="e1495-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="e1495-170">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="e1495-170">Fixed issues:</span></span>
* <span data-ttu-id="e1495-171">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="e1495-171">Generic Web Services:</span></span>
 * <span data-ttu-id="e1495-172">W przypadku zmiany adresu URL usługi hello w domyślnym SAP wsconfig projektów za pomocą narzędzia do konfiguracji usługi sieci Web, a następnie sytuacji hello następujący błąd: nie można odnaleźć części ścieżki hello</span><span class="sxs-lookup"><span data-stu-id="e1495-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="e1495-173">Ogólny LDAP:</span><span class="sxs-lookup"><span data-stu-id="e1495-173">Generic LDAP:</span></span>
 * <span data-ttu-id="e1495-174">Łącznik GLDAP nie widzieć wszystkie atrybuty w usług AD LDS</span><span class="sxs-lookup"><span data-stu-id="e1495-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="e1495-175">Podziały kreatora po wykryciu żadnych atrybutów nazwy UPN od schematu katalogu LDAP hello</span><span class="sxs-lookup"><span data-stu-id="e1495-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="e1495-176">Delta importów niepowodzeniem z powodu błędów odnajdywania nie występuje podczas pełnego importu, gdy atrybut "objectclass" nie jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="e1495-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="e1495-177">Stronę konfiguracji "Konfiguruj partycje i hierarchie" nie wyświetla żadnych obiektów, który typ jest równy toohello partycji dla nowych serwerów w hello ogólny</span><span class="sxs-lookup"><span data-stu-id="e1495-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="e1495-178">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="e1495-178">LDAP MA.</span></span> <span data-ttu-id="e1495-179">Pokazują one tylko obiekty z partycji RootDSE.</span><span class="sxs-lookup"><span data-stu-id="e1495-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="e1495-180">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="e1495-180">Generic SQL:</span></span>
 * <span data-ttu-id="e1495-181">Napraw dla znaku wodnego ogólnego SQL usterki atrybutu wielowartościowego niezaimportowanych Import zmian</span><span class="sxs-lookup"><span data-stu-id="e1495-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="e1495-182">Podczas eksportowania deleted\added wartości atrybutu wielowartościowego, nie są one deleted\added w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="e1495-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="e1495-183">Program Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="e1495-183">Lotus Notes:</span></span>
 * <span data-ttu-id="e1495-184">Określone pole "Pełna nazwa" jest wyświetlany w magazynie metaverse hello poprawnie jednak eksportowanie tooNotes hello wartość dla atrybutu hello po wartości Null lub jest pusta.</span><span class="sxs-lookup"><span data-stu-id="e1495-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="e1495-185">Usuń zduplikowane Certifier błędu</span><span class="sxs-lookup"><span data-stu-id="e1495-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="e1495-186">W przypadku wybrania hello obiektu bez żadnych danych na powitania łącznika programu Lotus Domino z innymi obiektami następnie Otrzymaliśmy hello odnajdywania błędu podczas wykonywania pełnego importu.</span><span class="sxs-lookup"><span data-stu-id="e1495-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="e1495-187">Gdy Import zmian jest była uruchomiona na powitania łącznika programu Lotus Domino na końcu tego działania, hello hello usługi Microsoft.IdentityManagement.MA.LotusDomino.Service.exe czasami zwraca błąd aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1495-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="e1495-188">Członkostwo w grupach ogólną działa prawidłowo i jest obsługiwany, ale podczas uruchamiania hello eksportu tootry tooremove użytkownika z członkostwa pokazuje pomyślnym przeprowadzeniu z aktualizacją, ale faktycznie nie pobrać usunąć użytkownika hello z członkostwa programu Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="e1495-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="e1495-189">Tryb toochoose możliwość eksportowania jako "Dołącz element u dołu" został dodany w konfiguracji graficznego interfejsu użytkownika programu Lotus MA tooappend nowych elementów u dołu podczas eksportowania hello atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="e1495-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="e1495-190">Łącznik spowoduje to dodanie hello potrzebne logiki toodelete hello plik z folderu poczty hello i identyfikator magazynu.</span><span class="sxs-lookup"><span data-stu-id="e1495-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="e1495-191">Usuń członkostwa nie pracuje w cross NAB elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="e1495-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="e1495-192">Wartości, które powinny być pomyślnie usunięte z atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="e1495-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="e1495-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="e1495-193">1.1.117.0</span></span>
<span data-ttu-id="e1495-194">Wydanie: 2016 marca</span><span class="sxs-lookup"><span data-stu-id="e1495-194">Released: 2016 March</span></span>

<span data-ttu-id="e1495-195">**Nowy łącznik**</span><span class="sxs-lookup"><span data-stu-id="e1495-195">**New Connector**</span></span>  
<span data-ttu-id="e1495-196">Początkowa wersja hello [ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="e1495-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="e1495-197">**Nowe funkcje:**</span><span class="sxs-lookup"><span data-stu-id="e1495-197">**New features:**</span></span>

* <span data-ttu-id="e1495-198">Ogólny łącznik LDAP:</span><span class="sxs-lookup"><span data-stu-id="e1495-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="e1495-199">Dodano obsługę import zmian z Isode.</span><span class="sxs-lookup"><span data-stu-id="e1495-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="e1495-200">Łącznik usług sieci Web:</span><span class="sxs-lookup"><span data-stu-id="e1495-200">Web Services Connector:</span></span>
  * <span data-ttu-id="e1495-201">Zaktualizowano hello csEntryChangeResult działania i setImportErrorCode działania tooallow obiektu błędy na poziomie toobe zwrócony toohello wstecz aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="e1495-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="e1495-202">Zaktualizowano hello SAP6 i SAP6User szablony toouse hello nowy błąd poziomu funkcji obiektu.</span><span class="sxs-lookup"><span data-stu-id="e1495-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="e1495-203">Programu Lotus Domino łącznika:</span><span class="sxs-lookup"><span data-stu-id="e1495-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="e1495-204">Eksportu należy co certifier na książce adresowej.</span><span class="sxs-lookup"><span data-stu-id="e1495-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="e1495-205">Można teraz Użyj hello samo hasło dla wszystkich wydających świadectwa toomake hello zarządzania łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="e1495-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="e1495-206">**Rozwiązane problemy:**</span><span class="sxs-lookup"><span data-stu-id="e1495-206">**Fixed issues:**</span></span>

* <span data-ttu-id="e1495-207">Ogólny łącznik LDAP:</span><span class="sxs-lookup"><span data-stu-id="e1495-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="e1495-208">Dla IBM Tivoli DS niektóre atrybuty odwołania nie został wykryty poprawnie.</span><span class="sxs-lookup"><span data-stu-id="e1495-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="e1495-209">Dla usługi LDAP otwarte podczas importowania różnicowych odstępy na powitania początek i koniec ciągów została obcięta.</span><span class="sxs-lookup"><span data-stu-id="e1495-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="e1495-210">Novell i NetIQ eksportu przeniesiona obiektu między jednostkami organizacyjnymi/kontenerów i na powitania sam czasu obiektu hello zmienioną nazwę nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="e1495-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="e1495-211">Łącznik usług sieci Web:</span><span class="sxs-lookup"><span data-stu-id="e1495-211">Web Services Connector:</span></span>
  * <span data-ttu-id="e1495-212">Jeśli usługa sieci web hello miał wiele punkty końcowe dla tego samego powiązania, następnie hello łącznika nie poprawnie wykrył te punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="e1495-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="e1495-213">Programu Lotus Domino łącznika:</span><span class="sxs-lookup"><span data-stu-id="e1495-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="e1495-214">Eksport hello Pełna nazwa atrybutu tooa w poczty bazy danych zakończyło się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e1495-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="e1495-215">Eksport, który zarówno dodania i usunięcia elementu członkowskiego z grupy, tylko do wyeksportowanego hello dodane elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="e1495-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="e1495-216">Jeśli dokument o wersji jest nieprawidłowy (isValid atrybutu hello Ustaw toofalse), następnie hello łącznika kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e1495-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="e1495-217">Starsze wersje</span><span class="sxs-lookup"><span data-stu-id="e1495-217">Older releases</span></span>
<span data-ttu-id="e1495-218">Przed marca 2016 hello łączników zostały wydane jako tematy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="e1495-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="e1495-219">**Ogólny LDAP**</span><span class="sxs-lookup"><span data-stu-id="e1495-219">**Generic LDAP**</span></span>

* <span data-ttu-id="e1495-220">[KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, września 2015</span><span class="sxs-lookup"><span data-stu-id="e1495-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="e1495-221">[KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, marca 2015 roku</span><span class="sxs-lookup"><span data-stu-id="e1495-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="e1495-222">[KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, stycznia 2015</span><span class="sxs-lookup"><span data-stu-id="e1495-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="e1495-223">[KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="e1495-224">[KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, marca 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="e1495-225">**Usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="e1495-225">**WebServices**</span></span>

* <span data-ttu-id="e1495-226">[KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="e1495-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e1495-227">**PowerShell**</span></span>

* <span data-ttu-id="e1495-228">[KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="e1495-229">**Programu Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="e1495-229">**Lotus Domino**</span></span>

* <span data-ttu-id="e1495-230">[KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, września 2015</span><span class="sxs-lookup"><span data-stu-id="e1495-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="e1495-231">[KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, marca 2015 roku</span><span class="sxs-lookup"><span data-stu-id="e1495-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="e1495-232">[KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, sierpnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="e1495-233">[KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, luty 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e1495-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="e1495-234">[KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, październik 2013</span><span class="sxs-lookup"><span data-stu-id="e1495-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="e1495-235">[KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, sierpnia 2013</span><span class="sxs-lookup"><span data-stu-id="e1495-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1495-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1495-236">Next steps</span></span>
<span data-ttu-id="e1495-237">Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e1495-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="e1495-238">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="e1495-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
