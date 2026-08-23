# Slot

Regras de negócio da entidade **Slot**

* Um Slot pertence a um `Local` e, transitivamente, a um `Event`.
* O horário de um Slot deve estar contido no intervalo de início e término do `Event`.
* Dois Slots do mesmo `Local` não podem se sobrepor no tempo.
* Um Slot só pode ser preenchido por, no máximo, uma `Proposal` aprovada.
* Um Slot só é compatível com uma `Proposal` cuja duração caiba dentro da duração do Slot.
* Apenas o papel `ORGANIZADOR` pode cadastrar um Slot.
