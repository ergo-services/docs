---
description: Что такое behavior
---

# Behavior

Термином behavior называются готовые к использованию дизайн-паттерны. Например, [`gen.Server`](../generic-behaviors/server/), [`gen.Supervisor`](../generic-behaviors/supervisor.md) и [`gen.Application`](../generic-behaviors/application.md). Они являются дизайн-паттернами общего назначения.  Также, в Ergo Framework на базе `gen.Server` реализованы специализированные дизайн-паттерны: [`gen.Stage`](../generic-behaviors/server/stage.md), [`gen.Saga`](../generic-behaviors/server/saga.md) и [`gen.Raft`](../generic-behaviors/server/raft.md).&#x20;

Теримин behavior был унаследован из Erlang и, чтобы избежать путаницы в терминологии, в дальнейшем будем использовать только его.

В Ergo Framework термин behavior применяется к объекту, реализующему базовый интерфейс `gen.ProcessBehavior`. Он требует от объекта реализации всего двух методов

```go
type ProcessBehavior interface {
	ProcessInit(Process, ...etf.Term) (ProcessState, error)
	ProcessLoop(ProcessState, chan<- bool) string
}
```

Все готовые к использованию behavior уже имеют реализацию этих методов, поэтому вам нет необходимости заниматься их реализацией.  Однако, они расширяют этот интерфейс своими методами.&#x20;

Например, реализация `gen.Server` определяет интефейс `gen.ServerBehavior`, который имеет не только встренный `gen.ProcessBehavior`, но и дополнительные методы - `Init`, `HandleCast`, `HandleCall`, `HandleInfo`, `Terminate`. Чтобы облегчить использование `gen.Server` и не заставлять разработчика реализовывать все  методы `gen.ServerBehavior`, в `gen.Server` уже присутствует их реализация, но с нулевым функционалом ("заглушки").&#x20;

Обращайте внимание на описание используемого behavior интерфейса. Некоторые реализации обязывают наличие реализации тих или иных методов. Это, конечно, зависит от логики используемого behavior. В частности, behavior `gen.Raft` определяет интерфейс `gen.RaftBehavior` обязывающий вас реализовать три метода `InitRaft`, `HandleAppend` и `HandleGet`, при этом остальные методы являются опциональными.

В любом случае, если вы не реализуете какой-либо из обязательных методов, при попытке запустить процесс вы получите ошибку. Например, для `gen.Raft` вы получите `"Raft: not a RaftBehavior"`, а для `gen.Saga` - `"Saga: not a SagaBehavior"`.

Как реализовать реализовать свой behavior смотрите раздел Custom Behavior. Вам также может быть интересным посмотреть пример, предлагаемый в директории [examples/gendemo](https://github.com/ergo-services/ergo/tree/master/examples/gendemo).







