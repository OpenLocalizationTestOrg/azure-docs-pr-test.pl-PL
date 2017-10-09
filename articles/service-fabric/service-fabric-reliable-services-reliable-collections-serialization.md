---
title: "aaaReliable serializacji obiektu kolekcji w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Azure serializacji obiektu kolekcji niezawodnej sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Niezawodne serializacji obiektu kolekcji w sieci szkieletowej usług Azure
Niezawodne kolekcje replikacji i utrwalić ich elementów toomake się, że są one trwałego na błędy maszyn i awarie zasilania.
Elementy zarówno tooreplicate i toopersist, niezawodne kolekcje muszą tooserialize je.

Niezawodne kolekcje Pobierz hello odpowiedni serializator dla danego typu z niezawodnej Menedżer stanów.
Menedżer stanu niezawodny zawiera wbudowane serializatorów i umożliwia toobe serializatorów niestandardowych zarejestrowany dla danego typu.

## <a name="built-in-serializers"></a>Wbudowane serializatorów

Menedżer stanu niezawodny obejmuje wbudowane serializatora dla niektórych typowych tak, aby serializować wydajnie domyślnie. Dla innych typów, Menedżer stanu niezawodnej powraca toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Wbudowane serializatorów są bardziej wydajne, ponieważ wiedzieli, nie można zmienić ich typów i nie potrzebują oni tooinclude informacje o typie hello, takie jak jego nazwa typu.

Menedżer stanu niezawodny ma wbudowane serializatora dla następujących typów: 
- Identyfikator GUID
- wartość logiczna
- Bajtów
- sbyte —
- Byte]
- char
- Ciąg
- Decimal
- O podwójnej precyzji
- Float
- int
- uint
- długa
- ulong
- krótki
- ushort

## <a name="custom-serialization"></a>Niestandardowej serializacji

Serializatorów niestandardowe są często używane tooincrease wydajności lub tooencrypt hello danych za pośrednictwem hello przewodowy i na dysku. Wśród innych przyczyn serializatorów niestandardowe są często bardziej efektywne niż ogólny serializator, ponieważ nie potrzebują tooserialize informacje o typie hello. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) jest używane tooregister niestandardowego programu szeregującego dla danego typu T. hello Rejestracja powinno się zdarzyć w konstrukcji hello hello StatefulServiceBase tooensure czy przed rozpoczęciem odzyskiwania, wszystkie kolekcje niezawodnej mają dostęp do tooread odpowiedni serializator toohello utrwalonych danych.

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> Niestandardowe serializatorów są pierwszeństwo nad serializatorów wbudowanych. Na przykład po zarejestrowaniu niestandardowego programu szeregującego dla int jest liczb całkowitych tooserialize używane zamiast hello wbudowanych serializatora dla int.

### <a name="how-tooimplement-a-custom-serializer"></a>Jak tooimplement serializatora niestandardowego

Serializatora niestandardowego wymaga tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfejsu.

> [!NOTE]
> IStateSerializer<T> zawiera przeciążenia dla zapisu i odczytu, która przyjmuje w dodatkowych T jako wartości podstawowej. Ten interfejs API jest różnicowej serializacji. Obecnie funkcja różnicowej serializacji nie jest widoczne. W związku z tym te dwa przeciążenia nie są nazywane, dopóki różnicowej serializacji jest widoczne i włączone.

Poniżej przedstawiono przykład typu niestandardowego o nazwie OrderKey, który zawiera cztery właściwości

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

Poniżej przedstawiono przykład stosowania IStateSerializer<OrderKey>.
Należy pamiętać, że odczytywanie i zapisywanie przeciążeń, które przyjmują w baseValue, wywołania ich odpowiednich przeciążenia dla zgodności wyszukiwanie do przodu.

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a>Możliwość
W [aplikacji uaktualnienia stopniowego](service-fabric-application-upgrade.md), uaktualnienie hello jest stosowane tooa podzbioru węzłów, domeny uaktualnienia pojedynczo. W trakcie tego procesu będzie niektórych domen uaktualnienia w nowszej wersji aplikacji hello, a niektóre domen uaktualnienia musi być na powitania starszej wersji aplikacji. Podczas fazy hello hello nowej wersji aplikacji musi być możliwe tooread hello starą wersję danych, a hello starą wersję aplikacji musi być możliwe tooread hello nowej wersji danych. Jeśli format danych hello nie jest zgodny, uaktualnienie hello do przodu i do tyłu może zakończy się awarią lub gorsza, dane mogą być utracone lub uszkodzony.

Jeśli korzystasz z wbudowanych serializator, nie masz tooworry o zgodności.
Jednak jeśli używasz niestandardowego programu szeregującego lub hello DataContractSerializer hello danych ma toobe nieograniczonej Wstecz i przekazuje zgodne.
Innymi słowy każda wersja programu szeregującego wymaga tooserialize stanie toobe oraz zdeserializować dowolnej wersji hello typu.

Użytkownicy kontraktu danych powinien być zgodny hello reguły dobrze zdefiniowany kontroli wersji, dodawanie, usuwanie i zmiana pola. Kontrakt danych ma również obsługę zajmujących się nieznany pól, przechwytywanie procesem hello serializacji i deserializacji i zajmujących się dziedziczenia klas. Aby uzyskać więcej informacji, zobacz [kontraktu danych przy użyciu](https://msdn.microsoft.com/library/ms733127.aspx).

Użytkownicy niestandardowego programu szeregującego przestrzegać toohello wytycznymi serializator hello używają toomake się, że jest Wstecz i przekazuje zgodne.
Typowy sposób obsługi wszystkich wersji jest dodawanie informacji o rozmiarze na początku hello i tylko dodanie właściwości opcjonalnych.
W ten sposób każdej wersji mogą odczytywać, jaka może i przejść przez hello pozostała część hello strumienia.

## <a name="next-steps"></a>Następne kroki
  * [Serializacja i uaktualniania](service-fabric-application-upgrade-data-serialization.md)
  * [Dokumentacja dla deweloperów niezawodnej kolekcji](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.
  * [Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.
  * Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).
  * Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).
  * Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).
