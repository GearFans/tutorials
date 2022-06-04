
### 事件

```rs
// pallets/gear/src/lib.rs

pub enum Event<T: Config> {
  /// Log event from the specific program.
  Log(StoredMessage),

  /// Program created and an init message enqueued.
  InitMessageEnqueued(MessageInfo),

  /// Program initialization error.
  InitFailure(MessageInfo, Reason),

  /// Program initialized.
  InitSuccess(MessageInfo),

  /// Dispatch message with a specific ID enqueued for processing.
  DispatchMessageEnqueued(MessageInfo),

  /// Dispatched message has resulted in an outcome
  MessageDispatched(DispatchOutcome),

  /// Some number of messages processed.
  // TODO: will be replaced by more comprehensive stats
  MessagesDequeued(u32),

  /// Value and gas has been claimed from a message in mailbox by the addressee
  ClaimedValueFromMailbox(MessageId),

  /// A message has been added to the wait list
  AddedToWaitList(StoredDispatch),

  /// A message has been removed from the wait list
  RemovedFromWaitList(MessageId),

  /// Program code with a calculated code hash is saved to the storage
  CodeSaved(H256),

  /// Pallet associated storage has been wiped.
  DatabaseWiped,

  /// Message was not executed
  MessageNotExecuted(MessageId),
}
```

### 获取事件

```js
const gearApi = await GearApi.create({
  providerAddress: "wss://rpc-node.gear-tech.io"
});

// subscribeToLogEvents
gearApi.gearEvents.subscribeToLogEvents(({ data: { id, source, payload, reply } }) => {
  console.log(`------subscribeToLogEvents-----`)

  console.log(`
    Log:
      messageId: ${id.toHex()}
      from program: ${source.toHex()}
      payload: ${payload.toJSON()}
    ${
      reply.isSome ? `reply to: ${reply.unwrap()[0].toHex()}
      with error: ${reply.unwrap()[1].toNumber() === 0 ? false : true}
      `: ''}
  `);
});

// subscribeToProgramEvents
gearApi.gearEvents.subscribeToProgramEvents(({ method, data: { info, reason } }) => {
  console.log(`------subscribeToProgramEvents-----`)

  console.log(`
      ${method}:
      programId: ${info.programId.toHex()}
      initMessageId: ${info.messageId.toHex()}
      origin: ${info.origin.toHex()}
      ${reason ? `reason: ${JSON.stringify(reason)}` : ''}
      ${reason ? `reason: ${reason.toHuman()}` : ''}
  `);
});
```