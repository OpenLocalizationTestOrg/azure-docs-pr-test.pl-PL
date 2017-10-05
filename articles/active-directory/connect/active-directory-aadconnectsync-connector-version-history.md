---
title: "Historia wersji łącznika | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę wszystkich wersji łączników dla programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM)"
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
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="04458-103">Historia wersji łącznika</span><span class="sxs-lookup"><span data-stu-id="04458-103">Connector Version Release History</span></span>
<span data-ttu-id="04458-104">Łączników programu Forefront Identity Manager (FIM) i Microsoft Identity Manager (MIM) są często aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="04458-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="04458-105">Ten temat dotyczy tylko programu FIM i MIM.</span><span class="sxs-lookup"><span data-stu-id="04458-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="04458-106">Te łączniki nie są obsługiwane dla instalacji na Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="04458-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="04458-107">Wydanych łączników są preinstalowane na AADConnect w przypadku uaktualniania do kompilacji.</span><span class="sxs-lookup"><span data-stu-id="04458-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="04458-108">Ten temat zawiera wszystkie wersje łączników, które zostały wydane.</span><span class="sxs-lookup"><span data-stu-id="04458-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="04458-109">Linki pokrewne:</span><span class="sxs-lookup"><span data-stu-id="04458-109">Related links:</span></span>

* [<span data-ttu-id="04458-110">Pobierz najnowsze łączników</span><span class="sxs-lookup"><span data-stu-id="04458-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="04458-111">[Ogólny łącznik LDAP](active-directory-aadconnectsync-connector-genericldap.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="04458-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="04458-112">[Ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="04458-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="04458-113">[Łącznik usług Web](http://go.microsoft.com/fwlink/?LinkID=226245) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="04458-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="04458-114">[Łącznik programu PowerShell](active-directory-aadconnectsync-connector-powershell.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="04458-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="04458-115">[Łącznika programu Lotus Domino](active-directory-aadconnectsync-connector-domino.md) odwołania dokumentacji</span><span class="sxs-lookup"><span data-stu-id="04458-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="04458-116">1.1.604.0 (AADConnect do czasu zwolnienia)</span><span class="sxs-lookup"><span data-stu-id="04458-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="04458-117">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="04458-117">Fixed issues:</span></span>

* <span data-ttu-id="04458-118">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="04458-118">Generic Web Services:</span></span>
  * <span data-ttu-id="04458-119">Rozwiązano problem uniemożliwia tworzone podczas wystąpiły co najmniej dwa punkty końcowe projektu protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="04458-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="04458-120">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="04458-120">Generic SQL:</span></span>
  * <span data-ttu-id="04458-121">W operacji importu GSQL został nie konwertowania czasu poprawnie, podczas zapisywania do przestrzeni łącznika.</span><span class="sxs-lookup"><span data-stu-id="04458-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="04458-122">Domyślny format daty i godziny przestrzeni łącznika GSQL został zmieniony z "RRRR MM-dd: ssZ" na "RRRR MM-dd: ssZ".</span><span class="sxs-lookup"><span data-stu-id="04458-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="04458-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="04458-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="04458-124">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="04458-124">Fixed issues:</span></span>

* <span data-ttu-id="04458-125">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="04458-125">Generic Web Services:</span></span>
  * <span data-ttu-id="04458-126">Narzędzie Wsconfig nie zostały przekonwertowane poprawnie tablicy Json z "przykładowe żądanie" dla metody usługi REST.</span><span class="sxs-lookup"><span data-stu-id="04458-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="04458-127">Przyczyną problemów z serializacji tej tablicy Json dla żądania REST.</span><span class="sxs-lookup"><span data-stu-id="04458-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="04458-128">Narzędzie konfiguracji łącznika usług sieci Web nie obsługuje użycia miejsca symboli w nazwach atrybutów JSON</span><span class="sxs-lookup"><span data-stu-id="04458-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="04458-129">Wzorzec podstawienia można dodać ręcznie do pliku WSConfigTool.exe.config, np.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="04458-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="04458-130">Program Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="04458-130">Lotus Notes:</span></span>
  * <span data-ttu-id="04458-131">Gdy opcja **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** jest wyłączony łącznik zakończy się niepowodzeniem podczas eksportu (aktualizacja) po przepływu eksportu wszystkie atrybuty zostaną wyeksportowane do Domino, ale w czasie eksportu KeyNotFoundException jest zwracana do synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="04458-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="04458-132">Dzieje się tak, ponieważ operacja zmiany nazwy nie powiodło się, gdy próbuje zmienić nazwy domeny (atrybut nazwy użytkownika), zmieniając jeden z atrybutów poniżej:</span><span class="sxs-lookup"><span data-stu-id="04458-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="04458-133">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="04458-133">LastName</span></span>
      - <span data-ttu-id="04458-134">Imię</span><span class="sxs-lookup"><span data-stu-id="04458-134">FirstName</span></span>
      - <span data-ttu-id="04458-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="04458-135">MiddleInitial</span></span>
      - <span data-ttu-id="04458-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="04458-136">AltFullName</span></span>
      - <span data-ttu-id="04458-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="04458-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="04458-138">jednostki organizacyjnej</span><span class="sxs-lookup"><span data-stu-id="04458-138">ou</span></span>
      - <span data-ttu-id="04458-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="04458-139">altcommonname</span></span>

  * <span data-ttu-id="04458-140">Gdy **Zezwalaj na niestandardowe wydających świadectwa dla jednostki organizacyjnej/organizacji** opcja jest włączona, ale wydających świadectwa wymagane są nadal puste, a następnie KeyNotFoundException występuje.</span><span class="sxs-lookup"><span data-stu-id="04458-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="04458-141">Ulepszenia:</span><span class="sxs-lookup"><span data-stu-id="04458-141">Enhancements:</span></span>

* <span data-ttu-id="04458-142">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="04458-142">Generic SQL:</span></span>
  * <span data-ttu-id="04458-143">**Scenariusz: przeprojektowany implementowany:** "*" funkcji</span><span class="sxs-lookup"><span data-stu-id="04458-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="04458-144">**Opis rozwiązania:** zmienić podejście do [Obsługa atrybuty wielowartościowe odwołanie](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="04458-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="04458-145">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="04458-145">Fixed issues:</span></span>

* <span data-ttu-id="04458-146">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="04458-146">Generic Web Services:</span></span>
  * <span data-ttu-id="04458-147">Nie można zaimportować konfigurację serwera, jeśli znajduje się łącznik usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="04458-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="04458-148">Łącznik usługi sieci Web nie działa z wieloma usługami sieci Web</span><span class="sxs-lookup"><span data-stu-id="04458-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="04458-149">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="04458-149">Generic SQL:</span></span>
  * <span data-ttu-id="04458-150">Brak typów obiektu są wyświetlane pojedynczą wartość atrybutu do którego istnieje odwołanie</span><span class="sxs-lookup"><span data-stu-id="04458-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="04458-151">Import zmian śledzenia zmian wartość zostanie usunięty z tabeli wielowartościowych obiektu usuwa strategii</span><span class="sxs-lookup"><span data-stu-id="04458-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="04458-152">Overflowexception — w łączniku GSQL z bazy danych DB2 na AS / 400</span><span class="sxs-lookup"><span data-stu-id="04458-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="04458-153">Program Lotus:</span><span class="sxs-lookup"><span data-stu-id="04458-153">Lotus:</span></span>
  * <span data-ttu-id="04458-154">Dodano możliwość enable\disable wyszukiwanie jednostki organizacyjne przed otwarciem GlobalParameters strony</span><span class="sxs-lookup"><span data-stu-id="04458-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="04458-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="04458-155">1.1.443.0</span></span>

<span data-ttu-id="04458-156">Wydanie: 2017 marca</span><span class="sxs-lookup"><span data-stu-id="04458-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="04458-157">Ulepszenia</span><span class="sxs-lookup"><span data-stu-id="04458-157">Enhancements</span></span>

* <span data-ttu-id="04458-158">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="04458-158">Generic SQL:</span></span></br><span data-ttu-id="04458-159">
  **Scenariusz symptomy:** jest dobrze znane ograniczenie z łącznikiem SQL, w którym możemy tylko Zezwalaj na odwołanie do typu jeden obiekt i wymagają odwołań z elementami członkowskimi.</span><span class="sxs-lookup"><span data-stu-id="04458-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="04458-160">
**Opis rozwiązania:** w kroku przetwarzania dla odwołania "*" zostanie wybrana opcja, wszystkich kombinacji typów obiektów zostaną zwrócone do aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="04458-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="04458-161">Spowoduje to utworzenie wielu symboli zastępczych</span><span class="sxs-lookup"><span data-stu-id="04458-161">This will create many placeholders</span></span>
- <span data-ttu-id="04458-162">Jest on wymagany do upewnij się, że nazwy są unikatowe między typami obiektów.</span><span class="sxs-lookup"><span data-stu-id="04458-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="04458-163">Ogólny LDAP:</span><span class="sxs-lookup"><span data-stu-id="04458-163">Generic LDAP:</span></span></br><span data-ttu-id="04458-164">
 **Scenariusz:** po wybraniu kilku kontenerów w określonej partycji, następnie wyszukiwania nadal będzie realizowane w całej partycji.</span><span class="sxs-lookup"><span data-stu-id="04458-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="04458-165">Właściwe będą filtrowane przez usługę synchronizacji, ale nie MA, co może spowodować obniżenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="04458-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="04458-166">**Opis rozwiązania:** zmienić GLDAP łącznika kod, aby była możliwa przejdź przez wszystkie kontenery i wyszukiwania obiektów w każdej z nich, zamiast wyszukiwanie w całej partycji.</span><span class="sxs-lookup"><span data-stu-id="04458-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="04458-167">Programu Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="04458-167">Lotus Domino:</span></span>

  <span data-ttu-id="04458-168">**Scenariusz:** Domino poczty usunięcia obsługę usunięcie osoby podczas eksportowania.</span><span class="sxs-lookup"><span data-stu-id="04458-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="04458-169">
  **Rozwiązanie:** obsługi usuwania można skonfigurować poczty do usunięcia osoby, podczas eksportowania.</span><span class="sxs-lookup"><span data-stu-id="04458-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="04458-170">Rozwiązane problemy:</span><span class="sxs-lookup"><span data-stu-id="04458-170">Fixed issues:</span></span>
* <span data-ttu-id="04458-171">Usługi sieci Web ogólne:</span><span class="sxs-lookup"><span data-stu-id="04458-171">Generic Web Services:</span></span>
 * <span data-ttu-id="04458-172">W przypadku zmiany domyślnego adresu URL usługi SAP wsconfig projektów za pomocą narzędzia do konfiguracji usługi sieci Web, a następnie wystąpił następujący błąd: nie można odnaleźć części ścieżki</span><span class="sxs-lookup"><span data-stu-id="04458-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="04458-173">Ogólny LDAP:</span><span class="sxs-lookup"><span data-stu-id="04458-173">Generic LDAP:</span></span>
 * <span data-ttu-id="04458-174">Łącznik GLDAP nie widzieć wszystkie atrybuty w usług AD LDS</span><span class="sxs-lookup"><span data-stu-id="04458-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="04458-175">Podziały kreatora po wykryciu żadnych atrybutów nazwy UPN od schematu katalogu LDAP</span><span class="sxs-lookup"><span data-stu-id="04458-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="04458-176">Delta importów niepowodzeniem z powodu błędów odnajdywania nie występuje podczas pełnego importu, gdy atrybut "objectclass" nie jest zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="04458-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="04458-177">Stronę konfiguracji "Konfiguruj partycje i hierarchie" nie wyświetla żadnych obiektów typu jest równa partycji dla nowych serwerów w ogólnej</span><span class="sxs-lookup"><span data-stu-id="04458-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="04458-178">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="04458-178">LDAP MA.</span></span> <span data-ttu-id="04458-179">Pokazują one tylko obiekty z partycji RootDSE.</span><span class="sxs-lookup"><span data-stu-id="04458-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="04458-180">Ogólny SQL:</span><span class="sxs-lookup"><span data-stu-id="04458-180">Generic SQL:</span></span>
 * <span data-ttu-id="04458-181">Napraw dla znaku wodnego ogólnego SQL usterki atrybutu wielowartościowego niezaimportowanych Import zmian</span><span class="sxs-lookup"><span data-stu-id="04458-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="04458-182">Podczas eksportowania deleted\added wartości atrybutu wielowartościowego, nie są one deleted\added w źródle danych.</span><span class="sxs-lookup"><span data-stu-id="04458-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="04458-183">Program Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="04458-183">Lotus Notes:</span></span>
 * <span data-ttu-id="04458-184">Określone pole "Pełna nazwa" jest wyświetlane w magazynie metaverse poprawnie jednak podczas eksportowania notatek wartość atrybutu ma wartość Null lub pusty.</span><span class="sxs-lookup"><span data-stu-id="04458-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="04458-185">Usuń zduplikowane Certifier błędu</span><span class="sxs-lookup"><span data-stu-id="04458-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="04458-186">W przypadku wybrania obiekt bez żadnych danych łącznika programu Lotus Domino z innymi obiektami następnie Otrzymaliśmy błąd odnajdywania podczas wykonywania pełnego importu.</span><span class="sxs-lookup"><span data-stu-id="04458-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="04458-187">Gdy Import zmian jest była uruchomiona łącznika programu Lotus Domino na końcu tego przebiegu Microsoft.IdentityManagement.MA.LotusDomino.Service.exe usługi czasami zwraca błąd aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04458-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="04458-188">Członkostwo w grupach ogólną działa prawidłowo i jest obsługiwany, ale podczas uruchamiania eksportu, aby spróbować usunąć użytkownika z członkostwa są wyświetlane pomyślnym przeprowadzeniu z aktualizacją, ale faktycznie nie pobrać usunąć użytkownika z członkostwa programu Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="04458-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="04458-189">Pozwala wybrać tryb eksportu "Dołącz element u dołu" został dodany w konfiguracji graficznego interfejsu użytkownika programu Lotus MA dołączyć nowe elementy u dołu podczas eksportowania dla atrybutów wielowartościowych.</span><span class="sxs-lookup"><span data-stu-id="04458-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="04458-190">Łącznik spowoduje dodanie logiki potrzebne do Usuń plik z folderu poczty i identyfikator magazynu.</span><span class="sxs-lookup"><span data-stu-id="04458-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="04458-191">Usuń członkostwa nie pracuje w cross NAB elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="04458-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="04458-192">Wartości, które powinny być pomyślnie usunięte z atrybutu wielowartościowego</span><span class="sxs-lookup"><span data-stu-id="04458-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="04458-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="04458-193">1.1.117.0</span></span>
<span data-ttu-id="04458-194">Wydanie: 2016 marca</span><span class="sxs-lookup"><span data-stu-id="04458-194">Released: 2016 March</span></span>

<span data-ttu-id="04458-195">**Nowy łącznik**</span><span class="sxs-lookup"><span data-stu-id="04458-195">**New Connector**</span></span>  
<span data-ttu-id="04458-196">Początkowa wersja [ogólny Łącznik usług SQL](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="04458-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="04458-197">**Nowe funkcje:**</span><span class="sxs-lookup"><span data-stu-id="04458-197">**New features:**</span></span>

* <span data-ttu-id="04458-198">Ogólny łącznik LDAP:</span><span class="sxs-lookup"><span data-stu-id="04458-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="04458-199">Dodano obsługę import zmian z Isode.</span><span class="sxs-lookup"><span data-stu-id="04458-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="04458-200">Łącznik usług sieci Web:</span><span class="sxs-lookup"><span data-stu-id="04458-200">Web Services Connector:</span></span>
  * <span data-ttu-id="04458-201">Zaktualizowano csEntryChangeResult a działaniem setImportErrorCode umożliwia błędów poziomu obiekt ma zostać zwrócony aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="04458-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="04458-202">Zaktualizowano SAP6 SAP6User szablonów i korzystać z nowych funkcji błąd poziomu obiektu.</span><span class="sxs-lookup"><span data-stu-id="04458-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="04458-203">Programu Lotus Domino łącznika:</span><span class="sxs-lookup"><span data-stu-id="04458-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="04458-204">Eksportu należy co certifier na książce adresowej.</span><span class="sxs-lookup"><span data-stu-id="04458-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="04458-205">Można teraz używać tego samego hasła dla wszystkich wydających świadectwa aby ułatwić zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="04458-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="04458-206">**Rozwiązane problemy:**</span><span class="sxs-lookup"><span data-stu-id="04458-206">**Fixed issues:**</span></span>

* <span data-ttu-id="04458-207">Ogólny łącznik LDAP:</span><span class="sxs-lookup"><span data-stu-id="04458-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="04458-208">Dla IBM Tivoli DS niektóre atrybuty odwołania nie został wykryty poprawnie.</span><span class="sxs-lookup"><span data-stu-id="04458-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="04458-209">Dla usługi LDAP otwarte podczas importowania różnicowych białe znaki na początku i na końcu ciągów została obcięta.</span><span class="sxs-lookup"><span data-stu-id="04458-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="04458-210">Novell i NetIQ eksportu przeniesiona obiektu między jednostkami organizacyjnymi/kontenery i w tym samym czasie, należy zmienić nazwy obiektu nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="04458-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="04458-211">Łącznik usług sieci Web:</span><span class="sxs-lookup"><span data-stu-id="04458-211">Web Services Connector:</span></span>
  * <span data-ttu-id="04458-212">Jeśli usługa sieci web ma wiele punkty końcowe dla tego samego powiązania, następnie łącznika nie poprawnie wykrył te punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="04458-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="04458-213">Programu Lotus Domino łącznika:</span><span class="sxs-lookup"><span data-stu-id="04458-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="04458-214">Eksport atrybutu imię i nazwisko poczty w bazie danych zakończyło się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="04458-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="04458-215">Export, która zarówno dodania i usunięcia elementu członkowskiego z grupy eksportowane tylko dodanych elementów.</span><span class="sxs-lookup"><span data-stu-id="04458-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="04458-216">Jeśli dokument o wersji jest nieprawidłowy (isValid atrybut ma wartość false), a następnie łącznika kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="04458-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="04458-217">Starsze wersje</span><span class="sxs-lookup"><span data-stu-id="04458-217">Older releases</span></span>
<span data-ttu-id="04458-218">Przed marca 2016 łączników zostały wydane jako tematy pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="04458-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="04458-219">**Ogólny LDAP**</span><span class="sxs-lookup"><span data-stu-id="04458-219">**Generic LDAP**</span></span>

* <span data-ttu-id="04458-220">[KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, września 2015</span><span class="sxs-lookup"><span data-stu-id="04458-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="04458-221">[KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, marca 2015 roku</span><span class="sxs-lookup"><span data-stu-id="04458-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="04458-222">[KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, stycznia 2015</span><span class="sxs-lookup"><span data-stu-id="04458-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="04458-223">[KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="04458-224">[KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, marca 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="04458-225">**Usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="04458-225">**WebServices**</span></span>

* <span data-ttu-id="04458-226">[KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="04458-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="04458-227">**PowerShell**</span></span>

* <span data-ttu-id="04458-228">[KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="04458-229">**Programu Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="04458-229">**Lotus Domino**</span></span>

* <span data-ttu-id="04458-230">[KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, września 2015</span><span class="sxs-lookup"><span data-stu-id="04458-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="04458-231">[KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, marca 2015 roku</span><span class="sxs-lookup"><span data-stu-id="04458-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="04458-232">[KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, sierpnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="04458-233">[KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, luty 2014 r.</span><span class="sxs-lookup"><span data-stu-id="04458-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="04458-234">[KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, październik 2013</span><span class="sxs-lookup"><span data-stu-id="04458-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="04458-235">[KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, sierpnia 2013</span><span class="sxs-lookup"><span data-stu-id="04458-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="04458-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04458-236">Next steps</span></span>
<span data-ttu-id="04458-237">Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="04458-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="04458-238">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="04458-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
