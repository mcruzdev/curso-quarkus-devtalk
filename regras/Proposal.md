# Proposal

Regras de negócio da entidade **Proposal**

* Uma Proposal só pode ser submetida pelo papel `SPEAKER`.
* Uma Proposal recém-submetida inicia com o status `SUBMETIDA`.
* Apenas os papéis `REVISOR` e `ORGANIZADOR` podem aprovar ou rejeitar uma Proposal.
* Ao ser aprovada, a Proposal deve ser alocada automaticamente a um `Slot` compatível e disponível, dentro da mesma transação da aprovação.
* Se não houver `Slot` compatível e disponível no momento da aprovação, a operação deve ser desfeita (rollback) e a Proposal permanece com o status `APROVADA_AGUARDANDO_SLOT`.
* Uma Proposal rejeitada não ocupa nenhum `Slot`.
* Toda mudança de status de uma Proposal deve gerar um evento publicado no Kafka.
* O `SPEAKER` deve ser notificado por e-mail sempre que o status da sua Proposal mudar.
