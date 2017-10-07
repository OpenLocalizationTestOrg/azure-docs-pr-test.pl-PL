---
title: aaaAccessing maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera | Dokumentacja firmy Microsoft
description: "Omówienie sposobu tooview tworzenie i zarządzanie nimi Azure maszynach wirtualnych (VM) w Eksploratorze serwera w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Uzyskiwanie dostępu do maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera
Za pomocą Eksploratora serwera w programie Visual Studio, można wyświetlić informacje o maszynach wirtualnych obsługiwanych przez platformę Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Uzyskiwanie dostępu do maszyn wirtualnych w Eksploratorze serwera
Jeśli masz maszyn wirtualnych hostowanych na platformie Azure, możesz uzyskiwać do nich dostęp w Eksploratorze serwera. Musisz zarejestrować w tooyour tooview subskrypcji platformy Azure Twojej usługi mobile services. toosign, otwórz menu skrótów hello hello Azure węzła w Eksploratorze serwera, a następnie wybierz pozycję **połączyć tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget informacji o maszynach wirtualnych
1. W Eksploratorze serwera wybierz maszynę wirtualną, a następnie wybierz tooshow klucza hello F4 okna właściwości.
   
    Witaj w poniższej tabeli przedstawiono właściwości, które są dostępne, ale są one wszystkich tylko do odczytu. toochange ich, użyj hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Właściwość | Opis |
   | --- | --- |
   | Nazwa DNS |adres URL Hello z hello adres internetowy hello maszyny wirtualnej. |
   | Środowisko |Dla maszyny wirtualnej hello wartość tej właściwości jest zawsze produkcji. |
   | Nazwa |Nazwa Hello hello maszyny wirtualnej. |
   | Rozmiar |rozmiar Hello hello maszynę wirtualną, która odzwierciedla hello ilość pamięci i miejsca na dysku, który jest dostępny. Aby uzyskać więcej informacji, zobacz jak: Konfigurowanie rozmiarów maszyn wirtualnych. |
   | Stan |Wartości obejmują uruchamianie, wprowadzenie, zatrzymywania, zatrzymane i pobierania stanu. Jeśli pojawi się podczas pobierania stanu, hello bieżący stan jest nieznany. Witaj wartości dla tej właściwości różnią się od wartości hello, które są używane na powitania [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | Identyfikator subskrypcji |Identyfikator subskrypcji Hello konta platformy Azure. Informacje te można wyświetlić na powitania [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885) wyświetlając hello właściwości dla subskrypcji. |
2. Wybierz węzeł punktu końcowego, a następnie Wyświetl hello **właściwości** okna.
3. Witaj poniższej tabeli opisano dostępne właściwości hello punktów końcowych, ale są one tylko do odczytu. tooadd lub Edytuj punkty końcowe hello maszyny wirtualnej, użyj hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Właściwość | Opis |
   | --- | --- |
   | Nazwa |Identyfikator hello punktu końcowego. |
   | Port prywatny |port Hello do aplikacji wewnętrznych tooyour dostępu do sieci. |
   | Protokół |używa protokołu Hello hello Warstwa transportu dla tego punktu końcowego, TCP lub UDP. |
   | Port publiczny |Witaj port używany dla aplikacji tooyour dostępu publicznego. |

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przy użyciu ról platformy Azure w programie Visual Studio, zobacz [za pomocą pulpitu zdalnego z rolami Azure](vs-azure-tools-remote-desktop-roles.md).

