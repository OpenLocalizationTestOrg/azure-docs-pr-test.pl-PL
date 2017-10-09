## <a name="scenario"></a>Scenariusz
toobetter pokazują, jak Udr toocreate tego dokumentu użyje scenariusz hello poniżej.

![OPIS ILUSTRACJI](./media/virtual-network-create-udr-scenario-include/figure1.png)

W tym scenariuszu utworzysz jeden przez dla hello *Front end podsieci* i przez inny dla hello *podsieci zakończenia Wstecz* , zgodnie z poniższym opisem: 

* **Frontonu przez**. Witaj frontonu przez zostaną zastosowane toohello *frontonu* podsieci i może zawierać jedną trasę:    
  * **RouteToBackend**. Tej trasy będzie wysyłał wszystkie ruchu toohello wewnętrzna podsieć toohello **FW1** maszyny wirtualnej.
* **Wewnętrznej bazy danych przez**. Hello zaplecza przez zostaną zastosowane toohello *zaplecza* podsieci i może zawierać jedną trasę:    
  * **RouteToFrontend**. Ta trasa będzie wysyłał wszystkie toohello podsieci frontonu toohello ruchu **FW1** maszyny wirtualnej.

Hello kombinację te trasy zapewni, że cały ruch kierowany z jednej podsieci tooanother będzie kierowany toohello **FW1** maszyny wirtualnej, która jest używana jako urządzenie wirtualne. Należy również tooturn na przesyłanie dalej IP dla tej maszyny Wirtualnej, tooensure może odbierać ruch kierowany tooother maszyn wirtualnych.

