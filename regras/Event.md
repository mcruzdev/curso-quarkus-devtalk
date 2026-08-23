# Event

Regras de negócio da entidade **Event**

* O horário de início do evento deve ser menor que o horário de término do evento.
* A horário de início do evento não deve estar no passado.
* Um Event deve ter pelo menos um `Local` cadastrado antes de receber `Slots`.
* Apenas o papel `ORGANIZADOR` pode cadastrar ou editar um Event.
