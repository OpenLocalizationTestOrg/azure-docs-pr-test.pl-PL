Jest ważne toorealize, że istnieją dwa sposoby tooconfigure odbiornik grupy dostępności na platformie Azure. sposoby Hello różnią się hello typu usługi równoważenia obciążenia Azure, używanego podczas tworzenia odbiornika hello. Witaj w poniższej tabeli opisano różnice hello:

| Typ usługi równoważenia obciążenia | Wdrażanie | Zastosowania: |
| --- | --- | --- |
| **Zewnętrzne** |Używa hello *publiczny wirtualny adres IP* usługi w chmurze hello obsługującego hello maszynach wirtualnych (VM). |Należy tooaccess hello odbiornika z hello poza siecią wirtualną, łącznie z hello Internet. |
| **Wewnętrzny** |Używa *wewnętrznego modułu równoważenia obciążenia* za pomocą prywatnego adresu dla odbiornika hello. |Można uzyskać dostępu do odbiornika hello tylko z wewnątrz hello tej samej sieci wirtualnej. Ten dostęp obejmuje sieci VPN typu lokacja lokacja w scenariuszach hybrydowych. |

> [!IMPORTANT]
> Dla odbiornika że używa usługi chmury hello publicznych adresów VIP (zewnętrznej usługi równoważenia obciążenia), tak długo, jak powitania klienta, odbiornik i bazy danych znajdują się w hello tego samego regionu Azure, nie będą naliczane opłaty za wyjście. W przeciwnym razie żadnych danych zwracany za pomocą hello odbiornika jest uważany za wyjście i jest rozliczana stawkami normalne transferu danych. 
> 
> 

ILB można skonfigurować tylko w sieciach wirtualnych z zakresu regionalnego. Istniejących sieci wirtualnych, które zostały skonfigurowane dla grupy koligacji nie można użyć ILB. Aby uzyskać więcej informacji, zobacz [Omówienie usługi równoważenia obciążenia wewnętrznego](../articles/load-balancer/load-balancer-internal-overview.md).

